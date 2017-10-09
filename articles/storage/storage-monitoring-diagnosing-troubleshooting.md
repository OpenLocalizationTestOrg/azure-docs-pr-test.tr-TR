---
title: "aaaMonitor, tanılama ve Azure Storage sorunlarını giderme | Microsoft Docs"
description: "Storage analytics, günlük, istemci-tarafı gibi kullanım özellikler ve diğer üçüncü taraf araçları tooidentify tanılamak ve Azure Storage ile ilgili sorunları giderme."
services: storage
documentationcenter: 
author: fhryo-msft
manager: jahogg
editor: tysonn
ms.assetid: d1e87d98-c763-4caa-ba20-2cf85f853303
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/11/2017
ms.author: fhryo-msft
ms.openlocfilehash: a33b3af7527223169be7cf3fed76c4765ff80e28
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-diagnose-and-troubleshoot-microsoft-azure-storage"></a>Microsoft Azure Storage izleme, tanılama ve sorun giderme
[!INCLUDE [storage-selector-portal-monitoring-diagnosing-troubleshooting](../../includes/storage-selector-portal-monitoring-diagnosing-troubleshooting.md)]

## <a name="overview"></a>Genel Bakış
Tanılama ve bulut ortamında bulunan bir dağıtılmış uygulama sorunlarını giderme geleneksel ortamlarda daha karmaşık olabilir. Uygulamalar şirket içinde bir mobil cihazda veya bileşiminden bir PaaS veya Iaas altyapısında dağıtılabilir. Genellikle, uygulamanızın ağ trafiği ortak ve özel ağlar geçiş yapabilir ve uygulamanızı Microsoft Azure depolama tabloları, Bloblar, kuyruklar gibi birden çok depolama teknolojileri kullanabilir veya toplama tooother veri dosyalarını depolayan gibi olarak ilişkisel ve belge veritabanları.

toomanage bu tür uygulamalar başarıyla, proaktif olarak izlemek ve anlamak nasıl toodiagnose ve bunları ve bunların bağımlı teknolojiler tüm yönlerini sorun giderme. Bir Azure Depolama Hizmetleri kullanıcı olarak, sürekli olarak, uygulamanızın kullandığı beklenmeyen değişiklikler (örneğin, normal yanıt süreleri daha yavaş) davranış hello depolama hizmetleri izlemek ve günlüğe kaydetme toocollect kullanmanız gerekir daha ayrıntılı veri ve tooanalyze bir derinlemesine sorun. hem izleme hem de günlük elde hello tanılama bilgileri karşılaştı, uygulamanızın vermek, toodetermine hello kök nedenini hello yardımcı olur. Merhaba sorunu gidermek ve hello uygun adımları atmanız tooremediate belirlemek. Azure depolama çekirdeği Azure hizmeti ve müşteriler toohello Azure altyapı dağıtma çözümleri hello çoğunluğu önemli bir parçasını oluşturur. Azure depolama özellikleri toosimplify izleme, tanılama ve depolama sorunlarını bulut tabanlı uygulamalar içerir.

> [!NOTE]
> Hello Azure File storage şu anda günlük kaydını desteklemiyor.
> 

Bir uygulamalı Kılavuzu tooend Azure Storage uygulamalarda sorun giderme uca için bkz: [uçtan uca Azure Storage ölçümleri ve günlüğe kaydetme, AzCopy ve ileti Çözümleyicisi'ni kullanarak sorun giderme](storage-e2e-troubleshooting.md).

* [Giriş]
  * [Bu kılavuz nasıl düzenlenir]
* [, depolama hizmet izlemesini]
  * [Hizmet durumu izleme]
  * [Kapasite izleme]
  * [Kullanılabilirlik izlemesi]
  * [Performans izleme]
* [depolama sorunları tanılama]
  * [Hizmet sistem durumu sorunları]
  * [Performans sorunları]
  * [Hatalarını tanılama]
  * [Depolama öykünücüsü sorunları]
  * [Depolama günlük araçları]
  * [Ağ günlük araçlarını kullanarak]
* [uçtan uca izleme]
  * [Günlük verileri ilişkilendirme]
  * [İstemci istek kimliği]
  * [sunucu istek kimliği]
  * [Zaman damgaları]
* [sorun giderme kılavuzluğu]
  * [ölçümleri Göster yüksek AverageE2ELatency ve düşük AverageServerLatency]
  * [Düşük AverageE2ELatency ve düşük AverageServerLatency ölçümleri göster ancak hello istemci yüksek gecikme yaşanıyor]
  * [Ölçümler yüksek AverageServerLatency gösteriyor]
  * [Kuyrukta ileti tesliminde beklenmeyen gecikmeler yaşıyorsunuz]
  * [ölçümleri Göster artışı içinde PercentThrottlingError]
  * [ölçümleri Göster artışı içinde PercentTimeoutError]
  * [Ölçümler PercentNetworkError’da artış gösteriyor]
  * [Merhaba istemci HTTP 403 (Yasak) iletileri alma]
  * [Merhaba istemci HTTP 404 (bulunamadı) iletileri alma]
  * [Merhaba istemci HTTP 409 (Çakışma) iletileri alma]
  * [ölçümleri Göster düşük PercentSuccess veya analytics günlük girişlerini sahip işlemler işlem durumu ClientOtherErrors]
  * [Kapasite ölçümlerini beklenmeyen artışı depolama kapasitesi kullanımı Göster]
  * [Çok sayıda ekli VHD'ler sahip sanal makinelerin beklenmeyen yeniden başlatmalar yaşıyor]
  * [Sorununuzu geliştirme veya test için hello storage öykünücüsü kullanarak ortaya çıkar.]
  * [.NET için Azure SDK'sı hello yüklerken sorunlarla karşılaşıyoruz]
  * [Bir depolama hizmetindeki farklı bir sorun olması]
  * [Windows ve Linux Azure File storage sorunlarını giderme](storage-troubleshoot-file-connection-problems.md)
* [ekler]
  * [ek 1: Fiddler toocapture HTTP ve HTTPS trafiği kullanılarak]
  * [ek 2: Wireshark toocapture ağ trafiğini kullanarak]
  * [ek 3: Microsoft Message Analyzer toocapture ağ trafiğini kullanarak]
  * [Ek 4: Excel kullanarak tooview ölçümleri ve günlük verileri]
  * [Ek 5: Visual Studio Team Services için Application Insights ile izleme]

## <a name="introduction"></a>Giriş
İlgili sorunlar, Azure Storage Analytics, istemci tarafı günlüğüne hello Azure Storage istemci kitaplığı ve diğer üçüncü taraf araçları tooidentify gibi toouse özelliklerini tanılamak ve Azure Storage sorunlarını giderme bu kılavuzu gösterir.

![][1]

Bu kılavuz öncelikli olarak Azure Storage Hizmetleri ve BT uzmanlarının gibi çevrimiçi hizmetlere yönetmekten sorumlu kullandığınız çevrimiçi hizmetlere geliştiriciler tarafından okunur hedeflenen toobe ' dir. Bu kılavuzun Hello hedefleri şunlardır:

* Merhaba sistem durumunu ve Azure Storage hesaplarınızı performansını korumak toohelp.
* tooprovide hello gerekli işlemleri ve araçları toohelp karar bir sorunu veya bir uygulamadaki sorun tooAzure depolama ilişkili değilse sizinle.
* tooAzure depolama sorunları çözmek için işlem yapılabilir rehberlik sizinle ilgili tooprovide.

### <a name="how-this-guide-is-organized"></a>Bu kılavuz nasıl düzenlenir
Merhaba bölüm "[, depolama hizmet izlemesini]" toomonitor nasıl hello sistem durumunu ve performansını Azure Storage Analytics ölçümleri (Storage ölçümleri) kullanarak, Azure depolama hizmetleri açıklar.

Merhaba bölüm "[depolama sorunları tanılama]" nasıl toodiagnose sorunları açıklar Azure Storage Analytics günlüğü (depolama oturum açma) kullanarak. Ayrıca nasıl tooenable kullanarak istemci tarafı günlük kaydı veya .NET için hello depolama istemci kitaplığı gibi hello istemci kitaplıklarından birini tesislerde hello Java için Azure SDK hello açıklar.

Merhaba bölüm "[uçtan uca izleme]" Merhaba bilgiler çeşitli günlük dosyalarını ve ölçüm verilerini nasıl ilişkilendirebilirsiniz açıklar.

Merhaba bölüm "[sorun giderme kılavuzluğu]" bazı, karşılaşabileceğiniz hello ortak depolama ile ilgili sorunları için sorun giderme kılavuzu sağlar.

Merhaba "[ekler]" Çözümleme ağ paket verileri, HTTP/HTTPS iletileri, çözümleme için fiddler'ı ve Microsoft Message Analyzer'ı ilişkilendirme için günlük verileri için Wireshark ve Netmon gibi diğer araçları kullanma hakkında bilgi içerir.

## <a name="monitoring-your-storage-service"></a>Depolama hizmet izleme
Windows performans izleme ile hakkında bilginiz varsa, depolama ölçümlerini Windows Performans İzleyicisi sayaçları Azure Storage denk olarak düşünebilirsiniz. Depolama ölçümleri ölçümleri (Windows Performans İzleyicisi terminolojisi sayaçları) hizmet kullanılabilirliği, istekleri tooservice toplam sayısı veya başarılı istekler tooservice yüzdesi gibi kapsamlı bir kümesini bulur. Merhaba kullanılabilir ölçümler tam bir listesi için bkz: [Storage Analytics Ölçüm tablosu şeması](http://msdn.microsoft.com/library/azure/hh343264.aspx). Merhaba depolama hizmeti toocollect ve birleşik ölçümleri her saat veya dakikada isteyip istemediğinizi belirtebilirsiniz. Depolama hesaplarınızı tooenable ölçümleri ve İzleyici nasıl görürüm hakkında daha fazla bilgi için [depolama ölçümlerini etkinleştirme ve ölçüm verilerini görüntüleme](http://go.microsoft.com/fwlink/?LinkId=510865).

Hangi saatlik ölçümleri seçebilirsiniz hello toodisplay istediğiniz [Azure portal](https://portal.azure.com) bir saatlik ölçümü belirli bir eşiği aştığında, yöneticilerin e-posta ile bildirim kuralları yapılandırın. Daha fazla bilgi için bkz: [uyarı bildirimleri alma](../monitoring-and-diagnostics/insights-receive-alert-notifications.md). 

Merhaba depolama hizmeti en iyi çaba kullanarak ölçümleri toplar, ancak her depolama işlemi kayıt.

Hello Azure portal, ölçümleri kullanılabilirlik, toplam istek sayısı ve bir depolama hesabı için ortalama gecikme süresi numaraları gibi görüntüleyebilirsiniz. Kullanılabilirlik belirli bir düzeyin altına düşerse bir bildirim kuralı da tooalert yönetici ayarlandı. Bu verileri görüntülemelerini, bir olası araştırma için hello tablo hizmeti başarı Oranı % 100 olan alanıdır (daha fazla bilgi için hello bölümüne bakın "[ölçümleri Göster düşük PercentSuccess veya analytics günlük girişlerini sahip işlemler işlem durumu ClientOtherErrors]").

Sürekli olarak sağlıklı ve tarafından beklendiği gibi gerçekleştirirken, Azure uygulamalarını tooensure izlemeniz gerekir:

* Toocompare geçerli verileri etkinleştirir ve önemli değişiklikler davranışlarındaki hello Azure depolama ve uygulamanızı tanımlamak bazı temel ölçümleri uygulaması oluşturma. taban çizgisi ölçümlerinizi Hello değerlerini çoğu durumda, uygulamaya özel olacaktır ve uygulamanızı test etme performans olduğunda bunları oluşturmanız gerekir.
* Dakika ölçümleri kaydetme ve bunları toomonitor etkin olarak beklenmeyen hatalar ve hata sayısı veya istek hızları ani gibi daha fazla bilgi için kullanma.
* Saatlik ölçümleri kaydı gibi toomonitor ortalama değerleri kullanarak hata sayıları ortalama ve istek hızları.
* Daha sonra hello bölümünde açıklandığı gibi tanılama araçlarını kullanarak olası sorunları Araştırıyor "[depolama sorunları tanılama]."

Görüntü aşağıdaki hello Hello grafiklerde nasıl hello için saatlik ölçümleri oluşan ortalama ani etkinliğinde gizleyebilirsiniz gösterilmektedir. Merhaba saatlik ölçümleri tooshow bir hızda isteklerinin gerçekleşmekte olan gerçekten hello dalgalanmaları ölçümleri ortaya hello dakika görünür.

![][3]

Merhaba Bu bölüm geri kalanı açıklar izlemek hangi ölçümleri ve neden.

### <a name="monitoring-service-health"></a>Hizmet durumu izleme
Merhaba kullanabilirsiniz [Azure portal](https://portal.azure.com) tooview hello durumunu tüm hello Depolama Birimi Hizmeti (ve diğer Azure hizmetleriyle) hello Merhaba Dünya Azure bölgeleri. Merhaba, uygulamanız için kullandığınız hello bölgede depolama hizmeti denetiminiz dışında bir sorun söz konusu ise bu toosee hemen sağlar.

Merhaba [Azure portal](https://portal.azure.com) hello etkileyen olayların bildirimleri çeşitli Azure hizmetlerine de sağlayabilirsiniz.
Not: Bu bilgiler hello hakkında geçmiş verileri birlikte önceden kullanılabilir [Azure hizmet Panosu'nu](http://status.azure.com).

Merhaba sırasında [Azure portal](https://portal.azure.com) toplar sistem durumu bilgilerinden içindeki Merhaba Azure veri merkezleri (Inside out izleme), bir dış bileşenini yaklaşım toogenerate yapay işlemler düzenli aralıklarla benimsenmesi düşünebilirsiniz Azure tarafından barındırılan web uygulamanız birden çok konumdan erişin. Merhaba tarafından sunulan hizmetlerin [Dynatrace](http://www.dynatrace.com/en/synthetic-monitoring) ve Visual Studio Team Services için Application Insights bu dışında yaklaşımın örnekler verilmiştir. Visual Studio Team Services için Application Insights hakkında daha fazla bilgi için bkz: hello ek "[ek 5: Visual Studio Team Services için Application Insights ile izleme](#appendix-5)."

### <a name="monitoring-capacity"></a>Kapasite izleme
Depolama ölçümleri BLOB'lar için hello en büyük oranda depolanan verilerin genellikle hesap çünkü hello blob hizmeti için kapasite ölçümlerini yalnızca depolar (Merhaba yazıldığı sırada, olası toouse Storage ölçümleri toomonitor hello kapasitesini tablolar ve Kuyruklar olmadığı) . Bu veriler hello bulabilirsiniz **$MetricsCapacityBlob** hello Blob hizmeti için izleme etkinleştirilirse tablo. Depolama ölçümleri günde bir kez bu verileri kaydeder ve hello hello değerini kullanabilirsiniz **RowKey** toodetermine hello satır toouser veri ilişkili bir varlık içerip içermediğini (değer **veri**) veya analytics veri ( değer **analytics**). Saklı her varlık hello kullanılan depolama alanı miktarı hakkında bilgi içerir (**kapasite** bayt cinsinden ölçülür) ve Merhaba kapsayıcılara geçerli sayısı (**ContainerCount**) ve blobları ( **ObjectCount**) hello depolama hesabı kullanımda. Hello depolanan hello kapasite ölçümleri hakkında daha fazla bilgi için **$MetricsCapacityBlob** tablo için bkz: [Storage Analytics Ölçüm tablosu şeması](http://msdn.microsoft.com/library/azure/hh343264.aspx).

> [!NOTE]
> Depolama hesabınızın hello kapasite limitlerini yaklaştığı erken bir uyarı için bu değerleri izlemeniz gerekir. Hello Azure portal, birleşik depolama kullanımı aşıyor ya da sizin eşiklerin altına düştüğünde belirttiğiniz uyarı kuralları toonotify ekleyebilirsiniz.
> 
> 

Merhaba blog gönderisi BLOB'ları gibi çeşitli depolama nesnelerinin Hello boyutunu tahmin etme Yardım için bkz [anlama Azure depolama faturalama – bant genişliği, işlemleri ve kapasite](http://blogs.msdn.com/b/windowsazurestorage/archive/2010/07/09/understanding-windows-azure-storage-billing-bandwidth-transactions-and-capacity.aspx).

### <a name="monitoring-availability"></a>Kullanılabilirlik izlemesi
Merhaba depolama hizmetleri hello kullanılabilirliğini hello hello değerinde izleyerek depolama hesabınızdaki izlemeniz gerekir **kullanılabilirlik** sütununda hello saat veya dakika ölçümleri tablolar — **$ MetricsHourPrimaryTransactionsBlob**, **$MetricsHourPrimaryTransactionsTable**, **$MetricsHourPrimaryTransactionsQueue**, **$ MetricsMinutePrimaryTransactionsBlob**, **$MetricsMinutePrimaryTransactionsTable**, **$MetricsMinutePrimaryTransactionsQueue**, **$ MetricsCapacityBlob**. Merhaba **kullanılabilirlik** sütun hello kullanılabilirliğini hello hizmet veya hello satır tarafından temsil edilen hello API işlemi gösteren bir yüzde değeri içeriyor (Merhaba **RowKey** hello satır içerip içermediğini gösterir Ölçümler bir bütün olarak hello hizmet veya belirli bir API işlemi).

% 100'değerinden küçük bir değer gösterir bazı depolama istekleri başarısız oluyor. Bunlar inceleyerek neden çözümleyemiyor görebilirsiniz hello sayıda farklı hata türleri ile isteği gibi göster hello ölçüm verilerini diğer sütunlardaki hello **ServerTimeoutError**. Toosee beklemelisiniz **kullanılabilirlik** gibi hello hizmet bölümleri toobetter Yük Dengeleme isteği hareket ederken geçici sunucu zaman aşımı nedeniyle geçici olarak % 100 aşağıda sonbaharda; hello istemci uygulamanızı mantığı yeniden dene Bu tür aralıklı koşullar işlemelidir. Merhaba makale [depolama Analytics günlüğe yazılan işlemler ve durum iletileri](http://msdn.microsoft.com/library/azure/hh343260.aspx) listeleri hello depolama ölçümlerini içerir işlem türleri kendi **kullanılabilirlik** hesaplama.

Merhaba, [Azure portal](https://portal.azure.com), uyarı kuralları toonotify ekleyebilirsiniz, varsa **kullanılabilirlik** hizmet belirttiğiniz bir eşiğin altına düşmesi için.

Merhaba "[sorun giderme kılavuzluğu]" bölümünde bu kılavuzun bazı ortak depolama hizmeti sorunları ilgili tooavailability açıklar.

### <a name="monitoring-performance"></a>Performans izleme
hello performansını hello depolama hizmetleri toomonitor, kullanabileceğiniz hello ölçümleri hello saatlik izleyerek ve ölçümleri tabloları dakika.

* Merhaba hello değerleri **AverageE2ELatency** ve **AverageServerLatency** sütunları göster hello ortalama süre hello depolama hizmeti veya API işlem türü tooprocess istekleri sürüyor. **AverageE2ELatency** tooread hello isteği geçen hello süre içeren uçtan uca gecikme ölçüsüdür ve ayrıca toohello geçen süre tooprocess hello istekte hello yanıt gönderme (Merhaba isteği sonra bu nedenle ağ gecikmesi içerir Merhaba depolama hizmeti ulaştığında); **AverageServerLatency** bir ölçüdür yalnızca hello işlem süresi ve bu nedenle ilgili herhangi bir ağ gecikmesi dışlar hello istemcisi ile toocommunicating. Merhaba bölümüne bakın "[ölçümleri Göster yüksek AverageE2ELatency ve düşük AverageServerLatency]" neden Tartışması için bu kılavuzda daha sonra bu iki değer arasında önemli bir fark olabilir.
* Merhaba hello değerleri **Totalıngress** ve **TotalEgress** depolama hizmetinizi dışında veya belirli bir API işlemi türü üzerinden giderek tooand içinde gelen sütunlar hello toplam veri miktarını bayt cinsinden gösterir.
* Merhaba hello değerleri **TotalRequests** Sütun Göster hello isteklerinin toplam sayısı, depolama birimi hizmeti API işleminin hello alma. **TotalRequests** hello hello depolama hizmeti aldığı isteklerinin toplam sayısı.

Genellikle, bu değerleri beklenmeyen değişiklikleri araştırma gerektiren bir sorun olduğunu bir göstergesi olarak izlenir.

Merhaba, [Azure portal](https://portal.azure.com), toonotify, bu hizmet için hello performans ölçümlerini varsa altına düşmesine veya belirttiğiniz bir eşiği aşması uyarı kuralı ekleyebilirsiniz.

Merhaba "[sorun giderme kılavuzluğu]" bölümünde bu kılavuzun bazı ortak depolama hizmeti sorunları ilgili tooperformance açıklar.

## <a name="diagnosing-storage-issues"></a>Depolama sorunları tanılama
Uygulamanızda bir sorun veya sorun uyumlu hale gelebilir çeşitli yollarla vardır, bunlar:

* Merhaba uygulama toocrash veya toostop çalışma neden önemli bir hata.
* İzlediğiniz hello önceki bölümde açıklandığı gibi hello ölçümleri temel değerlerinden önemli değişiklikler "[, depolama hizmet izlemesini]."
* Raporlar, uygulamanızın belirli bazı işleminin beklendiği gibi tamamlanmadığını kullanıcılardan veya bazı özelliği çalışmıyor.
* Uygulama içinde oluşturulan hatalar, günlük dosyalarında veya başka bir bildirim yöntem aracılığıyla görünür.

Genellikle, sorunları ilgili tooAzure depolama hizmetleri geniş dört kategoriden ayrılır:

* Uygulamanız, kullanıcılar tarafından bildirilen veya hello performans ölçümleri değişikliklerinden ortaya bir performans sorunu var.
* Bir veya daha fazla bölgelerde hello Azure Storage altyapı ile ilgili bir sorun yoktur.
* Uygulamanızı kullanıcılarınız tarafından bildirilen veya izlemenizi hello hata sayısı ölçümleri bir artış tarafından açığa hatayla karşılaşıyor.
* Geliştirme ve test sırasında hello yerel depolama öykünücüsü kullanarak; özellikle toousage hello depolama öykünücüsünü ile ilgili bazı sorunlarla karşılaşabilirsiniz.

Merhaba aşağıdaki bölümlerde toodiagnose izleyin ve her şu dört kategoriden sorunlarını giderme hello adımları verilmiştir. Merhaba bölüm "[sorun giderme kılavuzluğu]" Bu kılavuzda daha sonra karşılaşabileceğiniz bazı yaygın sorunlar için daha fazla ayrıntı sağlar.

### <a name="service-health-issues"></a>Hizmet sistem durumu sorunları
Hizmet durumu genellikle denetimi dışında sorunlardır. Merhaba [Azure portal](https://portal.azure.com) depolama hizmetleri de dahil olmak üzere Azure Hizmetleri ile devam eden sorunları hakkında bilgi sağlar. Depolama hesabınızı oluştururken okuma erişimli coğrafi olarak yedekli depolama için ettiyseniz, ardından hello olay hello birincil konumda kullanılabilir olan, verilerinizin uygulamanızı geçici olarak toohello salt okunur kopyasını hello ikincil konumdaki geçiş. toodo Bu, uygulamanızın mümkün tooswitch hello birincil ve ikincil depolama konumları kullanarak arasında olmalı ve salt okunur verilerle azaltılmış işlevsellik modunda mümkün toowork olması gerekir. Hello Azure Storage istemcisi kitaplıklarını toodefine birincil depolama biriminden okuma başarısız olursa, ikincil depolama biriminden okuyabilen bir yeniden deneme ilkesi izin verin. Uygulamanız da toobe hello veri hello ikincil konumdaki sonuçta tutarlı olduğunu kullanan gerekir. Daha fazla bilgi için bkz: hello blog gönderisi [Azure Depolama artıklık seçenekleri ve okuma erişimli coğrafi olarak yedekli depolama](https://blogs.msdn.microsoft.com/windowsazurestorage/2013/12/11/windows-azure-storage-redundancy-options-and-read-access-geo-redundant-storage/).

### <a name="performance-issues"></a>Performans sorunları
bir uygulamanın performansını Hello özellikle kullanıcı açısından öznel olabilir. Bu nedenle, önemli toohave temel ölçümleri kullanılabilir toohelp tanımlarsınız olduğu olabilir burada bir performans sorunu. Birçok faktöre bir Azure depolama hizmeti hello istemci uygulama açısından hello performansını etkileyebilir. Bu etkenler hello depolama birimi hizmeti, hello istemci veya hello ağ altyapısı çalışabilir; Bu nedenle önemli toohave hello performans sorunu hello kaynağını tanımlamak için bir strateji olur.

Hello ölçümleri hello performans sorunu hello nedeni büyük olasılıkla konumunu hello tanımladıktan sonra kullanım hello günlük dosyaları toofind hello daha fazla sorun giderme ve bilgi toodiagnose ayrıntılı sonra kullanabilirsiniz.

Merhaba bölüm "[sorun giderme kılavuzluğu]" ilgili bazı yaygın performans hakkında daha fazla bilgi sorunları daha sonra bu kılavuzdaki sağlar karşılaşabilirsiniz.

### <a name="diagnosing-errors"></a>Hatalarını tanılama
Uygulamanızın kullanıcılarının, hello istemci uygulaması tarafından bildirilen hataların bilgilendirebilirsiniz. Depolama ölçümleri de kaydeder, depolama hizmetleri farklı hata türlerinden sayısı gibi **NetworkError**, **ClientTimeoutError**, veya **AuthorizationError**. Depolama ölçümleri farklı hata türlerinin sayısı yalnızca kayıtları olsa da, sunucu tarafı, istemci tarafı ve ağ günlüklerini inceleyerek istekleri ayrı ayrı hakkında daha fazla ayrıntı elde edebilirsiniz. Genellikle, hello depolama hizmet tarafından döndürülen hello HTTP durum kodunu neden hello isteği başarısız göstergesidir verecektir.

> [!NOTE]
> Bazı aralıklı hatalar toosee beklemelisiniz unutmayın: Örneğin, tootransient ağ koşulları nedeniyle hatalar veya uygulama hataları.
> 
> 

Merhaba aşağıdaki kaynaklara depolama ilgili durum ve hata kodları anlamak için kullanışlıdır:

* [Ortak REST API hata kodları](http://msdn.microsoft.com/library/azure/dd179357.aspx)
* [BLOB hizmeti hata kodları](http://msdn.microsoft.com/library/azure/dd179439.aspx)
* [Kuyruk hizmeti hata kodları](http://msdn.microsoft.com/library/azure/dd179446.aspx)
* [Tablo hizmeti hata kodları](http://msdn.microsoft.com/library/azure/dd179438.aspx)
* [Dosya hizmeti hata kodları](https://msdn.microsoft.com/library/azure/dn690119.aspx)

### <a name="storage-emulator-issues"></a>Depolama öykünücüsü sorunları
Hello Azure SDK'sı bir geliştirme iş istasyonunda çalıştırabilirsiniz bir depolama öykünücüsü içerir. Bu öykünücüsü çoğu hello Azure storage Hizmetleri hello davranışını taklit eder ve geliştirme ve sınama sırasında faydalı olur, toorun etkinleştirme hello olmadan Azure storage hizmetleri kullanan uygulamaları bir Azure aboneliği ve Azure depolama hesabı için gerekir.

Merhaba "[sorun giderme kılavuzluğu]" bölümünde bu kılavuzun hello storage öykünücüsü kullanarak karşılaşılan bazı yaygın sorunları açıklar.

### <a name="storage-logging-tools"></a>Depolama günlük araçları
Depolama günlük depolama istekleri Azure depolama hesabınızdaki sunucu tarafı günlüğe kaydedilmesini sağlar. Tooenable sunucu tarafı günlüğe kaydetme ve erişim hello verileri nasıl oturum hakkında daha fazla bilgi için bkz: [depolama günlüğünü etkinleştirme ve erişim günlüğü verilerini](http://go.microsoft.com/fwlink/?LinkId=510867).

Merhaba .NET için depolama istemci kitaplığı, uygulamanız tarafından gerçekleştirilen toostorage işlemleri ilişkili toocollect istemci-tarafı günlük verilerini sağlar. Daha fazla bilgi için bkz: [istemci-tarafı .NET depolama istemci kitaplığı hello ile oturum](http://go.microsoft.com/fwlink/?LinkId=510868).

> [!NOTE]
> Bazı durumlarda (örneğin, SAS yetkilendirme hataları), bir kullanıcı için hiçbir istek verileri hello sunucu tarafı depolama günlüklerine bulabileceğiniz bir hata bildirebilir. Merhaba hello sorunun nedenini hello istemcide ise hello depolama istemci kitaplığı tooinvestigate hello günlüğe kaydetme özelliklerini kullanın veya ağ araçları tooinvestigate hello ağ izleme kullanın.
> 
> 

### <a name="using-network-logging-tools"></a>Ağ günlük araçlarını kullanarak
Ayrıntılı hello istemci ve sunucu tooprovide arasında hello trafiği yakalayabilir değişimi ve ağ koşulları altındaki hello hello veri hello istemci ve sunucu hakkında bilgi verilmiştir. Yararlı ağ günlük araçlarını içerir:

* [Fiddler](http://www.telerik.com/fiddler) tooexamine hello üstbilgileri ve HTTP ve HTTPS istek ve yanıt iletileri yükü verilerini sağlayan proxy hata ayıklama ücretsiz bir Web. Daha fazla bilgi için bkz: [ek 1: fiddler'ı kullanarak toocapture HTTP ve HTTPS trafiğini](#appendix-1).
* [Microsoft Ağ İzleyicisi'nin (Netmon)](http://www.microsoft.com/download/details.aspx?id=4865) ve [Wireshark](http://www.wireshark.org/) tooview etkinleştirmek protokol Çözümleyicileri ücretsiz ağı olan paket için ayrıntılı bilginin çok çeşitli ağ protokolleri. Wireshark hakkında daha fazla bilgi için bkz: "[ek 2: kullanarak Wireshark toocapture ağ trafiğini](#appendix-2)".
* Microsoft Message Analyzer Netmon ve ayrıca toocapturing paket verilerini ağ yerine geçen Microsoft aracından tooview yardımcı olur ve diğer Araçları'ndan yakalanan hello günlük verileri analiz ' dir. Daha fazla bilgi için "[ek 3: Microsoft Message Analyzer'ı kullanarak toocapture ağ trafiğini](#appendix-3)".
* Tooperform İstemci makinenizde hello ağ üzerinden toohello Azure depolama hizmeti bağlanabilir temel bağlantıyı test toocheck istiyorsanız, bu hello standardını kullanarak bunu yapamazsınız **ping** hello istemcide aracı. Ancak, hello kullanabilirsiniz [ **tcping** aracı](http://www.elifulkerson.com/projects/tcping.php) toocheck bağlantısı.

Çoğu durumda, depolama günlüğe kaydetme ve hello depolama istemci kitaplığı hello günlük verilerini yeterli toodiagnose bir sorun olacaktır, ancak bazı senaryolarda, ayrıntılı bu ağ günlük araçları sağlayan bilgi hello gerekebilir. Örneğin, Fiddler tooview kullanarak tooview üst bilgisi ve yük verileri tooand hello bir istemci uygulaması nasıl tooexamine sağlayacağı depolama hizmetleri gönderilen HTTP ve HTTPS iletileri etkinleştirir yeniden deneme depolama işlemleri. Protokol Çözümleyicileri Wireshark gibi paketleri ve bağlantı sorunları kayıp tootroubleshoot sağlayacağı tooview TCP veri etkinleştirme hello paket düzeyinde çalışır. İleti Çözümleyicisi hem HTTP hem de TCP katmanına çalışabilir.

## <a name="end-to-end-tracing"></a>Uçtan uca izleme
Uçtan uca izleme çeşitli günlük dosyalarını kullanarak olası sorunları Araştırıyor için kullanışlı bir tekniktir. Burada hello hello günlük dosyalarında arayan toostart hello sorunu gidermenize yardımcı olacak bilgiler ayrıntılı bir göstergesi olarak ölçümleri verilerinizden hello tarih/saat bilgileri kullanabilirsiniz.

### <a name="correlating-log-data"></a>Günlük verileri ilişkilendirme
İstemci uygulamaları günlüklerinden görüntülerken, ağ izler, ve bu günlüğü sunucu tarafı depolama birimi kritik toobe mümkün toocorrelate istekleri hello farklı günlük dosyaları. Merhaba günlük dosyalarını bağıntı tanımlayıcıları yararlı farklı alan sayısını içerir. Merhaba istemci istek kimliği hello en yararlı alan toouse toocorrelate girişlerini hello farklı günlüklerine ' dir. Ancak bazı durumlarda bu kullanışlı toouse olabilir hello sunucu istek kimliği veya zaman damgası. Merhaba aşağıdaki bölümler bu seçenekler hakkında daha fazla ayrıntı sağlar.

### <a name="client-request-id"></a>İstemci istek kimliği
Merhaba depolama istemci kitaplığı, benzersiz istemci istek kimliği her istek için otomatik olarak oluşturur.

* Hello depolama istemci kitaplığı hello istemci-tarafı günlük, hello istemci istek kimliği hello görünür oluşturur **istemci istek kimliği** toohello isteği ile ilgili her günlük girişinin alanı.
* İçinde ağ izleme bir Fiddler tarafından yakalanan gibi hello istemci istek kimliği hello içindeki istek iletileri görülebilir **x-ms-istemci-request-id** HTTP üstbilgisi değeri.
* Merhaba sunucu tarafı günlüğünde depolama günlüğü hello istemci istek kimliği hello istemci istek kimliği sütununda görüntülenir.

> [!NOTE]
> Birden çok istek tooshare hello için aynı istemci istek kimliği (Merhaba depolama istemci kitaplığı yeni bir değer otomatik olarak atar rağmen) hello istemci bu değer atanabilir olduğundan mümkündür. Yeniden deneme hello istemciden Hello durumda da, tüm girişimler hello paylaşmak aynı istemci istek kimliği. Merhaba istemciden gönderilen bir toplu Hello durumda hello toplu bir tek istemci istek kimliği vardır.
> 
> 

### <a name="server-request-id"></a>Sunucu istek kimliği
Merhaba depolama hizmeti sunucusu isteği kimlikleri otomatik olarak oluşturur.

* Merhaba sunucu tarafı günlüğüne depolama günlüğü hello sunucu istek kimliği hello görünür **istek kimliği üst bilgisi** sütun.
* İçinde ağ izleme bir Fiddler tarafından yakalanan gibi hello sunucu istek kimliği Yanıtı iletilerinde hello görünür **x-ms-request-id** HTTP üstbilgisi değeri.
* Hello depolama istemci kitaplığı hello istemci-tarafı günlük, hello sunucu istek kimliği hello görünür oluşturur **işlemi metin** hello sunucu yanıtı ayrıntılarını gösteren hello günlük girişi için sütun.

> [!NOTE]
> Her yeniden deneme girişimi hello istemciden ve bir toplu işlemde dahil her işlem benzersiz sunucu istek kimliği nedenle hello depolama hizmeti benzersiz bir sunucuyu aldığı, isteği kimlik tooevery isteği her zaman atar.
> 
> 

Merhaba depolama istemci kitaplığı döndürürse bir **StorageException** hello istemcisinde hello **RequestInformation** özelliği içeren bir **RequestResult** içeren nesnesinin bir **ServiceRequestID** özelliği. Aynı zamanda erişebilirsiniz bir **RequestResult** nesnesinin bir **OperationContext** örneği.

Aşağıdaki kod örneği Hello gösterir nasıl tooset özel bir **ClientRequestId** ekleyerek değeri bir **OperationContext** nesne hello isteği toohello depolama birimi hizmeti. Ayrıca gösterir nasıl tooretrieve hello **ServerRequestId** değeri hello yanıt iletisi.

```csharp
//Parse hello connection string for hello storage account.
const string ConnectionString = "DefaultEndpointsProtocol=https;AccountName=account-name;AccountKey=account-key";
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(ConnectionString);
CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();

// Create an Operation Context that includes custom ClientRequestId string based on constants defined within hello application along with a Guid.
OperationContext oc = new OperationContext();
oc.ClientRequestID = String.Format("{0} {1} {2} {3}", HOSTNAME, APPNAME, USERID, Guid.NewGuid().ToString());

try
{
    CloudBlobContainer container = blobClient.GetContainerReference("democontainer");
    ICloudBlob blob = container.GetBlobReferenceFromServer("testImage.jpg", null, null, oc);  
    var downloadToPath = string.Format("./{0}", blob.Name);
    using (var fs = File.OpenWrite(downloadToPath))
    {
        blob.DownloadToStream(fs, null, null, oc);
        Console.WriteLine("\t Blob downloaded toofile: {0}", downloadToPath);
    }
}
catch (StorageException storageException)
{
    Console.WriteLine("Storage exception {0} occurred", storageException.Message);
    // Multiple results may exist due tooclient side retry logic - each retried operation will have a unique ServiceRequestId
    foreach (var result in oc.RequestResults)
    {
            Console.WriteLine("HttpStatus: {0}, ServiceRequestId {1}", result.HttpStatusCode, result.ServiceRequestID);
    }
}
```

### <a name="timestamps"></a>Zaman damgaları
Zaman damgaları de kullanabilirsiniz toolocate ilgili günlük girişleri, ancak tüm saatinin hello istemciyle bulunabilecek sunucu arasında eğme dikkatli olun. Artı veya eksi hello istemci hello zaman damgasını temel sunucu tarafı girdileri eşleştirme için 15 dakika arama. Hello'hello blob içinde depolanan hello ölçümleri hello zaman aralığını kapsayan ölçümleri gösterir hello BLOB'lar için meta verileri blob unutmayın; Bu hello aynı saat veya dakika için birçok ölçümleri BLOB'lar varsa yararlı olur.

## <a name="troubleshooting-guidance"></a>Sorun giderme kılavuzu
Bu bölümde hello tanı koymaya yardımcı olur ve bazı hello yaygın sorunların çoğunu uygulamanızı sorun giderme hello Azure storage hizmetleri kullanırken karşılaşabileceğiniz. Toolocate hello bilgi ilgili tooyour belirli sorun aşağıda Hello listesini kullanın.

**Sorun giderme karar ağacı**

---
Sorununuzu hello depolama hizmetlerden biri toohello performansını ilişkilidir?

* [ölçümleri Göster yüksek AverageE2ELatency ve düşük AverageServerLatency]
* [Düşük AverageE2ELatency ve düşük AverageServerLatency ölçümleri göster ancak hello istemci yüksek gecikme yaşanıyor]
* [Ölçümler yüksek AverageServerLatency gösteriyor]
* [Kuyrukta ileti tesliminde beklenmeyen gecikmeler yaşıyorsunuz]

---
Sorununuzu hello depolama hizmetlerden biri toohello kullanılabilirliğini ilişkilidir?

* [ölçümleri Göster artışı içinde PercentThrottlingError]
* [ölçümleri Göster artışı içinde PercentTimeoutError]
* [Ölçümler PercentNetworkError’da artış gösteriyor]

---
 İstemci uygulamanız bir HTTP 4XX (örneğin, 404) yanıt Depolama hizmetinden alıyor?

* [Merhaba istemci HTTP 403 (Yasak) iletileri alma]
* [Merhaba istemci HTTP 404 (bulunamadı) iletileri alma]
* [Merhaba istemci HTTP 409 (Çakışma) iletileri alma]

---
[ölçümleri Göster düşük PercentSuccess veya analytics günlük girişlerini sahip işlemler işlem durumu ClientOtherErrors]

---
[Kapasite ölçümlerini beklenmeyen artışı depolama kapasitesi kullanımı Göster]

---
[Çok sayıda ekli VHD'ler sahip sanal makinelerin beklenmeyen yeniden başlatmalar yaşıyor]

---
[Sorununuzu geliştirme veya test için hello storage öykünücüsü kullanarak ortaya çıkar.]

---
[.NET için Azure SDK'sı hello yüklerken sorunlarla karşılaşıyoruz]

---
[Bir depolama hizmetindeki farklı bir sorun olması]

---
### <a name="metrics-show-high-AverageE2ELatency-and-low-AverageServerLatency"></a>Yüksek AverageE2ELatency ve düşük AverageServerLatency ölçümleri Göster
Merhaba hello aşağıda gösterimden [Azure portal](https://portal.azure.com) izleme aracı gösteren bir örnek hello burada **AverageE2ELatency** hello önemli ölçüde daha yüksek **AverageServerLatency**.

![][4]

Merhaba depolama hizmeti yalnızca hello ölçüm hesaplar Not **AverageE2ELatency** başarılı istekler için ve aksine **AverageServerLatency**, hello istemci toosend hello hello süresini içerir veri ve hello Depolama hizmetinden bildirim alırsınız. Bu nedenle, birbirinden **AverageE2ELatency** ve **AverageServerLatency** olabilir ya da toohello istemci uygulaması olması nedeniyle toorespond ya da son tooconditions hello ağdaki yavaş.

> [!NOTE]
> Ayrıca görüntüleyebilirsiniz **E2ELatency** ve **ServerLatency** hello depolama günlüğü tek depolama işlemleri için veri oturum.
> 
> 

#### <a name="investigating-client-performance-issues"></a>İstemci performans sorunlarını
Yavaş yanıt hello istemci için olası nedenler sınırlı sayıda kullanılabilir bağlantıları veya iş parçacığının olmamasına veya CPU, bellek veya ağ bant genişliği gibi kaynaklar yetersiz içerir. Merhaba istemci kodu toobe (örneğin zaman uyumsuz çağrılar toohello Depolama Birimi hizmetini kullanarak) daha verimli bir şekilde değiştirme veya daha büyük bir sanal makine (daha fazla sayıda çekirdek ve daha fazla bellek ile) kullanarak mümkün tooresolve hello sorun olabilir.

Merhaba tablo ve kuyruk Hizmetleri için hello Nagle algoritması de yüksek neden olabilir **AverageE2ELatency** çok karşılaştırıldığında gibi**AverageServerLatency**: sonrası hello daha fazla bilgi için bkz: [Nagle'nın Algoritmasıdır küçük isteklerini doğru değil kolay](http://blogs.msdn.com/b/windowsazurestorage/archive/2010/06/25/nagle-s-algorithm-is-not-friendly-towards-small-requests.aspx). Hello kullanarak hello Nagle algoritması kod devre dışı bırakabilirsiniz **ServicePointManager** hello sınıfında **System.Net** ad alanı. Bu, tüm çağrıları toohello tablo oluşturun veya zaten bağlantı etkilemez beri uygulamanızda sıra Hizmetleri'ni açmak önce yapmalısınız. Merhaba aşağıdaki örnek gelen hello **Application_Start** çalışan rolü yöntemi.

```csharp
var storageAccount = CloudStorageAccount.Parse(connStr);
ServicePoint tableServicePoint = ServicePointManager.FindServicePoint(storageAccount.TableEndpoint);
tableServicePoint.UseNagleAlgorithm = false;
ServicePoint queueServicePoint = ServicePointManager.FindServicePoint(storageAccount.QueueEndpoint);
queueServicePoint.UseNagleAlgorithm = false;
```

Hello istemci tarafı günlüklerini toosee kaç istemci uygulamanızı gönderme isteklerinin ve genel .NET için onay ilgili istemciniz CPU, .NET atık toplama, ağ kullanımı veya bellek gibi performans sorunları kontrol etmeniz gerekir. .NET istemci uygulamaları sorun giderme için başlangıç noktası olarak bkz [hata ayıklama, izleme ve profil oluşturma](http://msdn.microsoft.com/library/7fe0dd2y).

#### <a name="investigating-network-latency-issues"></a>Ağ gecikmesi sorunları araştırma
Genellikle tootransient koşullar nedeni hello ağ tarafından yüksek uçtan uca gecikme olur. Atılan paketlerin gibi her iki geçici ve kalıcı ağ sorunları Wireshark veya Microsoft Message Analyzer gibi araçları kullanarak araştırabilirsiniz.

Wireshark tootroubleshoot ağ sorunları kullanma hakkında daha fazla bilgi için bkz: "[ek 2: Wireshark toocapture ağ trafiğini kullanarak]."

Microsoft Message Analyzer tootroubleshoot ağ sorunları kullanma hakkında daha fazla bilgi için bkz: "[ek 3: Microsoft Message Analyzer toocapture ağ trafiğini kullanarak]."

### <a name="metrics-show-low-AverageE2ELatency-and-low-AverageServerLatency"></a>Düşük AverageE2ELatency ve düşük AverageServerLatency ölçümleri göster ancak hello istemci yüksek gecikme yaşanıyor
Bu senaryoda, hello en olası nedeni hello depolama hizmetine erişirken hello depolama istekleri gecikmeden oluşturur. Neden hello istemci gelen istekleri toohello blob hizmeti aracılığıyla kolaylaştırarak değil araştırmanız gerekir.

Kullanılabilir bağlantılar veya iş parçacığının sınırlı sayıda olan istekleri gönderirken geciktirme hello istemcisi için olası nedenlerden biri.

Ayrıca hello istemci birden çok deneme gerçekleştirme ve bu hello durumda hello nedeni araştırın olup olmadığını denetleyin. toodetermine hello istemci birden çok deneme gerçekleştiriyor olsun, şunları yapabilirsiniz:

* Merhaba Storage Analytics günlüklerini inceleyin. Birden çok deneme yapılmazsa, birden çok işlemleriyle görürsünüz aynı istemci istek kimliği hello ancak farklı sunucusuyla kimlikleri isteği.
* Merhaba istemci günlüklerini inceleyin. Ayrıntılı günlük kaydını yeniden deneme oluştuğunu gösterir.
* Kodunuzdaki hataları ayıklamanıza ve hello hello özelliklerini denetleyin **OperationContext** hello istekle ilişkili nesne. Merhaba işlemi denenirse hello **RequestResults** özelliği, birden çok benzersiz sunucu isteği kimlikleri içerecektir. Ayrıca, hello başlangıç denetleyin ve bitiş saatlerini her istek için. Merhaba kod örneği hello bölümünde daha fazla bilgi için bkz [sunucu istek kimliği].

Merhaba istemcisinde herhangi bir sorun varsa, paket kaybı gibi olası ağ sorunları araştırmanız gerekir. Wireshark veya Microsoft Message Analyzer tooinvestigate ağ sorunları gibi araçları kullanabilirsiniz.

Wireshark tootroubleshoot ağ sorunları kullanma hakkında daha fazla bilgi için bkz: "[ek 2: Wireshark toocapture ağ trafiğini kullanarak]."

Microsoft Message Analyzer tootroubleshoot ağ sorunları kullanma hakkında daha fazla bilgi için bkz: "[ek 3: Microsoft Message Analyzer toocapture ağ trafiğini kullanarak]."

### <a name="metrics-show-high-AverageServerLatency"></a>Yüksek AverageServerLatency ölçümleri Göster
Merhaba durumda yüksek **AverageServerLatency** blob indirme isteği için depolama günlüğü günlükleri toosee aynı blob (veya ayarlamak BLOB'ları) hello için yinelenen isteği yoksa hello kullanmanız gerekir. İçin BLOB karşıya yükleme isteklerini, hangi blok boyutu hello istemcisini kullanarak araştırmanız gereken (örneğin, hello okur sürece boyutu 64 K içinde ek yüklerini sonuçlanabilir daha az olan de buna blokları değerinden 64K öbekleri), ve birden çok istemciye karşıya yüklediğiniz engeller toohello aynı paralel olarak blob. İkinci ölçeklenebilirlik hedefleri başına hello aşan neden istekleri hello sayısında ani hello dakika başına ölçümlerini denetlemeniz gerekir: Ayrıca bkz. "[ölçümleri Göster artışı içinde PercentTimeoutError]."

Yüksek görüyorsanız **AverageServerLatency** blob yükleme istekleri için istekleri hello aynı blob veya BLOB'ları, bir dizi var. yinelenir, sonra Azure önbelleği kullanarak bu blob'lara önbelleğe almayı düşünün veya gerekir Azure içerik teslim hello Ağı (CDN). Karşıya yükleme istekleri için daha büyük bir blok boyutu kullanarak hello üretilen işi artırabilir. Sorguları tootables için de olası tooimplement istemci tarafı önbelleğe alma olduğu aynı sorgu işlemleri ve burada hello hello gerçekleştirmek istemcilerde verileri sık değiştirmez.

Yüksek **AverageServerLatency** değerleri hatalı tasarlanmış tabloları belirtisi de olabilir veya tarama işlemleri sonucunda ya da hello izleyin sorgular ekleme/başına koruma düzeni. Bkz: "[ölçümleri Göster artışı içinde PercentThrottlingError]" daha fazla bilgi için.

> [!NOTE]
> Kapsamlı denetim listesi Performans Denetim burada bulabilirsiniz: [Microsoft Azure depolama performans ve ölçeklenebilirlik Yapılacaklar listesi](storage-performance-checklist.md).
> 
> 

### <a name="you-are-experiencing-unexpected-delays-in-message-delivery"></a>Bir kuyruk iletisi Teslimde beklenmeyen gecikme yaşıyor
Hello saat arasında bir gecikme karşılaşıyorsanız bir ileti tooa kuyruk ve hello saati hello sırasından kullanılabilir tooread hale bir uygulama ekler ve ardından aşağıdaki adımları toodiagnose hello sorunu hello almanız gereken:

* Merhaba uygulaması başarıyla hello iletileri toohello sırası ekleme doğrulayın. Merhaba uygulaması hello denemeden değil kontrol edin **AddMessage** birkaç kez önce başarılı yöntemi. Merhaba depolama istemci kitaplığı günlükleri gerçekleştirdi tüm depolama işlemlerini gösterir.
* Saat eğriltme işlemde bir gecikme olur gibi hello ileti toohello sırası ve selamlama iletisine kolaylaştırır hello kuyruktaki iletileri okur hello çalışan rolü görünür ekler hello çalışan rolü arasında doğrulayın.
* Merhaba iletileri hello kuyruktaki iletileri okur hello çalışan rolü başarısız olup olmadığını denetleyin. Bir kuyruk istemci hello çağırırsa **GetMessage** yöntemi ancak bir bildirimle toorespond başarısız olursa, selamlama iletisine kalacak hello sırasına görünmez hello kadar **invisibilityTimeout** süresi sona erene. Bu noktada, selamlama iletisine yeniden işlemek için kullanılabilir hale gelir.
* Merhaba sırası uzunluğu bir zaman içinde artıyor denetleyin. Tüm hello iletileri diğer çalışanlarına hello sırasına yerleştirdiğinizi yeterli çalışanları kullanılabilir tooprocess yoksa bu durum oluşabilir. Silme isteklerinin başarısız olma ve hello gösterebilir iletileri sayısına dequeue, başarısız girişim toodelete selamlama iletisine hello ölçümleri toosee yinelenen de denetlemeniz gerekir.
* Beklenenden daha yüksek olan sıra işlemleri için Hello depolama günlüğü günlüklerini inceleyin **E2ELatency** ve **ServerLatency** normalden daha uzun bir zaman aralığında üzerinden değerleri.

### <a name="metrics-show-an-increase-in-PercentThrottlingError"></a>Ölçümleri artışı içinde PercentThrottlingError Göster
Bir depolama birimi hizmeti hello ölçeklenebilirlik hedefleri aşan azaltma hataları oluşur. Merhaba depolama hizmeti yapar bu tooensure, tek bir istemci ya da Kiracı hello hizmeti diğer hello gider kullanabilir. Daha fazla bilgi için bkz: [Azure Storage ölçeklenebilirlik ve performans hedefleri](storage-scalability-targets.md) depolama hesapları için ölçeklenebilirlik hedefleri ve depolama hesapları içindeki bölümler için performans hedefleri hakkında ayrıntılar için.

Merhaba, **PercentThrottlingError** ölçüm azaltma bir hata ile başarısız olan istek hello yüzdesi cinsinden artışı Göster, tooinvestigate iki senaryodan biri gerekir:

* [PercentThrottlingError geçici artış]
* [PercentThrottlingError hata kalıcı artış]

Bir artış **PercentThrottlingError** genellikle aynı zaman depolama istek hello sayısı artan olarak veya uygulamanızı test etme başlangıçta olduğunda yük hello sırasında oluşur. Bu ayrıca kendisini hello istemci "503 Sunucu meşgul" veya "500 işlem zaman aşımı" HTTP durum iletileri depolama işlemleri olarak bildiriminde.

#### <a name="transient-increase-in-PercentThrottlingError"></a>PercentThrottlingError geçici artış
Merhaba değeri ani görüyorsanız **PercentThrottlingError** Merhaba uygulaması yüksek etkinlik dönemleri ile çakıştığı, bir üstel (doğrusal değil) geri alma yeniden deneme stratejisini, istemci uygulamanız gerekir: Bu Merhaba hemen hello bölüm azaltmak ve ani trafiğinin çıkışı, uygulama toosmooth Yardım başlar. Nasıl tooimplement yeniden deneme ilkelerini kullanarak depolama istemci kitaplığı hello hakkında daha fazla bilgi için bkz: [Microsoft.WindowsAzure.Storage.RetryPolicies Namespace](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.retrypolicies.aspx).

> [!NOTE]
> Ani hello değeri de görebilirsiniz **PercentThrottlingError** , değil çakıştığı Merhaba uygulaması yüksek etkinlik dönemleri ile: Burada en olası nedeni hello bölümleri tooimprove yük taşıma hello depolama hizmeti nedir Dengeleme.
> 
> 

#### <a name="permanent-increase-in-PercentThrottlingError"></a>PercentThrottlingError hata kalıcı artış
Tutarlı bir şekilde yüksek bir değer için görüyorsanız **PercentThrottlingError** kalıcı bir artış işlem birimlerinizi veya ilk yükleme yaparken aşağıdaki sınamaları, uygulamanızda sonra tooevaluate gerekir Uygulamanızı depolama bölümleri nasıl kullandığını ve olup bir depolama hesabı için hello ölçeklenebilirlik hedefleri yaklaşıyor. (Tek bir bölümü olarak sayılır) bir sıranın hatalarda azaltma görüyorsanız, örneğin, daha sonra ek sıraları toospread hello işlemleri arasında birden çok bölüm kullanmayı düşünmelisiniz. Bir tabloda hatalar azaltma görüyorsanız, farklı bir bölümleme şeması toospread kullanarak tooconsider işlemlerinizi arasında birden çok bölüm geniş bir bölüm anahtarı değerlerini kullanarak gerekir. Bir ortak bu sorunun nedeni burada hello bölüm anahtarı olarak başlangıç tarihi seçin ve ardından belirli bir tarihte tüm veriler yazılır tooone bölüm hello başına/append koruma Desen: yük altında bu yazma tıkanıklığa neden olabilir. Farklı bir bölümleme tasarım düşünün veya blob storage kullanarak daha iyi bir çözüm olabilir olup olmadığını değerlendirmek. Merhaba azaltma trafiğinizi ani sonucunda oluşan ve istekleri desen düzgünleştirme yolları araştırmak de denetlemeniz gerekir.

Arasında birden çok bölüm işlemlerinizi dağıtırsanız, yine de hello depolama hesabı için ayarlanan hello ölçeklenebilirlik sınırları farkında olmalıdır. Örneğin, her işleme hello maksimum saniye başına 2.000 1 KB iletilerinin on sıraları kullandıysanız, hello olacaktır hello depolama hesabı için saniye başına 20.000 iletilerinin genel sınırı. Saniye başına birden fazla 20.000 varlıklar tooprocess ihtiyacınız varsa, birden çok depolama hesabı kullanmayı düşünmeniz gerekir. Ayrıca bu hello boyut, istekleri göz önünde bulundurmanız gerekir ve varlıkları hello depolama hizmeti istemcileriniz olduğunda kısıtlar üzerinde bir etkisi vardır: büyük istekleri ve varlıkları varsa, daha erken kısıtlanan.

Verimli sorgu tasarımı de toohit hello ölçeklenebilirlik sınırları tablo bölümleri için neden olabilir. Örneğin, bir sorgu, yalnızca bir yüzde hello varlıkların bir bölümünde seçer, ancak tüm hello varlıkları bir bölüme tarar bir filtre ile her varlık tooaccess gerekir. Bu bölümdeki işlemleri toplam sayısı hello doğru okuma her varlık sayar; Bu nedenle, hello ölçeklenebilirlik hedefleri kolayca erişebilir.

> [!NOTE]
> Performans testi herhangi verimsiz sorgu tasarımı, uygulamanızda ortaya çıkarır.
> 
> 

### <a name="metrics-show-an-increase-in-PercentTimeoutError"></a>Ölçümleri artışı içinde PercentTimeoutError Göster
Bir artış ölçümlerinizi Göster **PercentTimeoutError** depolama hizmetlerinizi biri için. Merhaba aynı zaman hello istemci depolama işlemlerinden yüksek hacimli "500 işlem zaman aşımı" HTTP durum iletilerini alır.

> [!NOTE]
> Bölüm tooa yeni bir sunucu taşıyarak yük bakiyelerini isteklerini zaman aşımı hataları hello depolama hizmeti geçici olarak görebilirsiniz.
> 
> 

Merhaba **PercentTimeoutError** ölçümüdür ölçümleri aşağıdaki hello toplamı: **ClientTimeoutError**, **AnonymousClientTimeoutError**,  **SASClientTimeoutError**, **ServerTimeoutError**, **AnonymousServerTimeoutError**, ve **SASServerTimeoutError**.

Merhaba sunucu zaman aşımı, hello sunucuda bir hata nedeniyle oluşur. Merhaba sunucu üzerinde bir işlemi hello istemci tarafından belirtilen hello zaman aşımı değeri aştığından hello istemci zaman aşımları gerçekleşir; Örneğin, hello depolama istemci kitaplığı kullanan bir istemci bir işlem için bir zaman aşımı hello kullanarak ayarlayabilirsiniz **ServerTimeout** hello özelliğinin **QueueRequestOptions** sınıfı.

Sunucu zaman aşımı daha fazla araştırma gerektiren hello depolama birimi hizmeti bir sorun olduğunu gösteriyor. Bu soruna neden trafiğinin herhangi bir ani hello ölçeklenebilirlik sınırları hello hizmeti ve tooidentify devreyi ölçümleri toosee kullanabilirsiniz. Merhaba zaman zaman ortaya çıkan bir sorundur, son olabilir hello hizmet tooload Dengeleme etkinliğinde. Merhaba sorun kalıcı ise ve hello ölçeklenebilirlik sınırları hello hizmetinin basarsa, uygulamanız tarafından neden değil, bir destek sorununu tetiklemelidir. İstemci zaman aşımları için hello zaman aşımı hello istemcisinde tooan uygun değere ayarlanır ve ya da değişiklik hello zaman aşımı değeri hello istemcisinde ayarlamak veya nasıl için hello depolama hizmetindeki hello işlemlerinin hello performansını geliştirebilir araştırmak karar vermeniz gerekir Tablo sorguları en iyi duruma getirme veya iletilerinizi hello boyutunun azaltılması örnek.

### <a name="metrics-show-an-increase-in-PercentNetworkError"></a>Ölçümleri artışı içinde PercentNetworkError Göster
Bir artış ölçümlerinizi Göster **PercentNetworkError** depolama hizmetlerinizi biri için. Merhaba **PercentNetworkError** ölçümüdür ölçümleri aşağıdaki hello toplamı: **NetworkError**, **AnonymousNetworkError**, ve  **SASNetworkError**. Merhaba istemci depolama istekte bulunduğunda hello depolama birimi hizmeti bir ağ hatası algıladığında, bu oluşur.

Merhaba bu hatanın en yaygın neden olan bir istemci hello depolama hizmetinde bir zaman aşımı süresi dolmadan önce bağlantısı kesiliyor. Neden ve ne zaman hello istemci hello depolama hizmet bağlantısını keser, istemci toounderstand içinde hello kod araştırmanız gerekir. Wireshark, Microsoft Message Analyzer veya Tcping tooinvestigate ağ bağlantısı sorunları hello istemciden de kullanabilirsiniz. Bu araçları hello açıklanan [ekler].

### <a name="the-client-is-receiving-403-messages"></a>Merhaba istemci HTTP 403 (Yasak) iletileri alma
İstemci uygulamanızın HTTP 403 (Yasak) hataları atma, olası bir nedeni (diğer olası nedenleri saat eğriltme, geçersiz anahtarları dahil ve boş olmasına karşın bir depolama istek gönderdiğinde hello istemci süresi dolmuş bir paylaşılan erişim imzası (SAS) kullanarak ise üst bilgiler). Süresi dolmuş bir SAS anahtarı hello neden olduğunda hello sunucu tarafı depolama günlüğü günlük verileri herhangi bir giriş görürsünüz değil. Merhaba aşağıdaki tabloda hello istemci-tarafı günlüğündeki depolama istemci Kitaplığı'de, bu sorunun oluşmasını gösterilmektedir hello tarafından oluşturulan bir örnek gösterilmektedir:

| Kaynak | Ayrıntı | Ayrıntı | İstemci istek kimliği | İşlemi metin |
| --- | --- | --- | --- | --- |
| Microsoft.WindowsAzure.Storage |Bilgi |3 |85d077ab-... |Konum modu PrimaryOnly başına birincil konumla işlemi başlatılıyor. |
| Microsoft.WindowsAzure.Storage |Bilgi |3 |85d077ab-... |Zaman uyumlu başlatma isteği toohttps://domemaildist.blob.core.windows.netazureimblobcontainer/blobCreatedViaSAS.txt?sv=2014-02-14&amp;sr c =&amp;si mypolicy =&amp;SIG OFnd4Rd7z01fIvh % 2BmcR6zbudIH2F5Ikm % = 2FyhNYZEmJNQ % 3B&amp;API sürümü 2014-02-14 =. |
| Microsoft.WindowsAzure.Storage |Bilgi |3 |85d077ab-... |Yanıtı bekleniyor. |
| Microsoft.WindowsAzure.Storage |Uyarı |2 |85d077ab-... |Yanıt bekleme sırasında özel durum oluştu: hello uzak sunucu bir hata döndürdü: (403) Yasak... |
| Microsoft.WindowsAzure.Storage |Bilgi |3 |85d077ab-... |Yanıtı alındı. Durum kodu 403, istek kimliği = 9d67c64a-64ed-4b0d-9515-3b14bbcdc63d, Content-MD5 = =, ETag =. |
| Microsoft.WindowsAzure.Storage |Uyarı |2 |85d077ab-... |Merhaba işlemi sırasında özel durum oluştu: hello uzak sunucu bir hata döndürdü: (403) Yasak... |
| Microsoft.WindowsAzure.Storage |Bilgi |3 |85d077ab-... |Merhaba işlem yeniden denetleniyor. Yeniden deneme sayısı = 0, HTTP durum kodu 403, özel durum = = hello uzak sunucusu bir hata döndürdü: (403) Yasak... |
| Microsoft.WindowsAzure.Storage |Bilgi |3 |85d077ab-... |Merhaba sonraki konumu hello konumu Modu'na bağlı tooPrimary ayarlandı. |
| Microsoft.WindowsAzure.Storage |Hata |1 |85d077ab-... |Yeniden deneme ilkesi için bir yeniden deneme izin vermedi. Başarısız olan hello uzak sunucusu ile bir hata döndürdü: (403) Yasak. |

Bu senaryoda, hello istemci hello belirteci toohello sunucu göndermeden önce hello SAS belirteci neden doluyor araştırmanız gerekir:

* Genellikle, istemci toouse için bir SAS hemen oluştururken bir başlangıç saati ayarlanmadı. Varsa küçük hello SAS oluşturarak hello ana bilgisayar arasındaki saat farklılıkları geçerli saati ve hello depolama hizmeti Merhaba, hello depolama hizmeti tooreceive henüz geçerli olmayan bir SAS mümkündür.
* Çok kısa süre sonu zamanı SAS ayarlamalısınız değil. Yeniden oluşturma hello konak küçük saat farklılıkları hello SAS ve hello depolama hizmeti tooa SAS açabilir görünüşe göre beklenenden daha önce süresi doluyor.
* Sürüm parametresi hello SAS anahtarı hello (örneğin **sv 2015-04-05 =**) eşleşme hello hello kullandığınız depolama istemci kitaplığı sürümü? Her zaman hello hello en son sürümünü kullanmanızı öneririz [depolama istemci Kitaplığı](https://www.nuget.org/packages/WindowsAzure.Storage/).
* Depolama erişim tuşlarınızı oluşturursanız, bu var olan tüm SAS belirteci geçersiz kılabilir. İstemci uygulamaları toocache için uzun süre sonu zamanı ile SAS belirteci oluşturursanız bu bir sorun olabilir.

Ardından hello depolama istemci kitaplığı toogenerate SAS belirteci kullanıyorsanız, kolay toobuild geçerli bir belirteci hale gelir. Ancak, hello Storage REST API'sini kullanarak ve el ile Merhaba SAS belirteci oluşturma hello konu dikkatle okumalısınız [paylaşılan erişim imzası için temsilci seçme erişimle](http://msdn.microsoft.com/library/azure/ee395415.aspx).

### <a name="the-client-is-receiving-404-messages"></a>Merhaba istemci HTTP 404 (bulunamadı) iletileri alma
Merhaba istemci uygulaması hello sunucusundan bir HTTP 404 (bulunamadı) iletisi alırsa, bu hello nesne hello istemci çalışırken gösterir (örneğin, bir varlık, tablo, blob, kapsayıcısı veya sıra) toouse hello depolama hizmetinde yok. Gibi bir dizi Bu, olası nedenleri vardır:

* [Merhaba istemci veya başka bir işlem daha önce silinmiş hello nesnesi]
* [Bir paylaşılan erişim imzası (SAS) yetkilendirme sorunu]
* [İstemci tarafı JavaScript kodu izin tooaccess hello nesnesi yok]
* [Ağ hatası]

#### <a name="client-previously-deleted-the-object"></a>Merhaba istemci veya başka bir işlem daha önce silinmiş hello nesnesi
Merhaba istemci tooread, update veya delete veri çoğunlukla bir depolama hizmetindeki nerede çalışıyor senaryolarda hello Depolama hizmetinden hello söz konusu Nesne silindi önceki bir işlemi hello sunucu tarafı kolay tooidentify günlüğe kaydeder. Çok sık hello günlük verileri, başka bir kullanıcı veya işlem silinen hello nesne gösterir. Merhaba sunucu tarafı günlüğüne depolama günlüğü hello işlem türü ve istenen nesnesi-anahtar sütun ne zaman bir istemci bir nesne silindi gösterir.

Hello istemci yeni bir nesne oluşturuyor koşuluyla, bu bir HTTP 404 (bulunamadı) yanıt olarak sonuçları neden bir istemci tooinsert bir nesne nerede çalışıyor hello senaryosunda, bunu hemen belirgin olmayabilir. Ancak, Hello istemci hello istemci mümkün toofind bir sıra olmalıdır bir ileti oluşturuyorsanız mümkün toofind hello blob kapsayıcısı, olmalıdır ve hello istemci satır ekleme, gereken bir blob oluşturuyorsanız mümkün toofind hello tablo olması gerekir.

Merhaba istemci-tarafı hello istemci toohello depolama birimi hizmeti belirli istekleri gönderirken bir anlayış ayrıntılıysa hello depolama istemci kitaplığı toogain günlüğünden kullanabilirsiniz.

Merhaba istemci için bunu oluşturmayı hello blob hello kapsayıcı bulamadığında hello hello depolama istemcisi kitaplığı tarafından oluşturulan aşağıdaki istemci-tarafı günlüğü hello sorun gösterilmektedir. Bu günlük depolama işlemleri aşağıdaki hello ayrıntılarını içerir:

| İstek Kimliği | İşlem |
| --- | --- |
| 07b26a5d-... |**DeleteIfExists** yöntemi toodelete hello blob kapsayıcısı. Bu işlem içeren Not bir **HEAD** hello kapsayıcı hello varlığı toocheck isteği. |
| e2d06d78... |**CreateIfNotExists** yöntemi toocreate hello blob kapsayıcısı. Bu işlem içeren Not bir **HEAD** hello hello kapsayıcı varlığını denetleyen istek. Merhaba **HEAD** 404 bir ileti döndürür ancak devam eder. |
| de8b1c3c-... |**UploadFromStream** yöntemi toocreate hello blob. Merhaba **PUT** istek 404 iletisiyle başarısız olur |

Günlük girişleri:

| İstek Kimliği | İşlemi metin |
| --- | --- |
| 07b26a5d-... |Eşzamanlı istek toohttps://domemaildist.blob.core.windows.net/azuremmblobcontainer başlatılıyor. |
| 07b26a5d-... |StringToSign HEAD...x-ms-client-request-id:07b26a5d-...x-ms-date:Tue, 03 Haz 2014 = 10:33:11 GMT.x-ms-version:2014-02-14./domemaildist/azuremmblobcontainer.restype:container. |
| 07b26a5d-... |Yanıtı bekleniyor. |
| 07b26a5d-... |Yanıtı alındı. Durum kodu 200, istek kimliği = eeead849... = Content-MD5 =, ETag = &quot;0x8D14D2DC63D059B&quot;. |
| 07b26a5d-... |Yanıt Üstbilgileri hello hello işlemi kalanıyla etmeden başarıyla işlendi. |
| 07b26a5d-... |Yanıt gövdesi yükleniyor. |
| 07b26a5d-... |İşlem başarıyla tamamlandı. |
| 07b26a5d-... |Eşzamanlı istek toohttps://domemaildist.blob.core.windows.net/azuremmblobcontainer başlatılıyor. |
| 07b26a5d-... |StringToSign DELETE...x-ms-client-request-id:07b26a5d-...x-ms-date:Tue, 03 Haz 2014 = 10:33:12 GMT.x-ms-version:2014-02-14./domemaildist/azuremmblobcontainer.restype:container. |
| 07b26a5d-... |Yanıtı bekleniyor. |
| 07b26a5d-... |Yanıtı alındı. Durum kodu 202, istek kimliği = 6ab2a4cf-..., Content-MD5 = =, ETag =. |
| 07b26a5d-... |Yanıt Üstbilgileri hello hello işlemi kalanıyla etmeden başarıyla işlendi. |
| 07b26a5d-... |Yanıt gövdesi yükleniyor. |
| 07b26a5d-... |İşlem başarıyla tamamlandı. |
| e2d06d78-... |Zaman uyumsuz istek toohttps://domemaildist.blob.core.windows.net/azuremmblobcontainer başlatılıyor.</td> |
| e2d06d78-... |StringToSign HEAD...x-ms-client-request-id:e2d06d78-...x-ms-date:Tue, 03 Haz 2014 = 10:33:12 GMT.x-ms-version:2014-02-14./domemaildist/azuremmblobcontainer.restype:container. |
| e2d06d78-... |Yanıtı bekleniyor. |
| de8b1c3c-... |Eşzamanlı istek toohttps://domemaildist.blob.core.windows.net/azuremmblobcontainer/blobCreated.txt başlatılıyor. |
| de8b1c3c-... |StringToSign PUT =... 64.qCmF+TQLPhq/YYK50mP9ZQ==...x-MS-BLOB-Type:BlockBlob.x-MS-Client-Request-id:de8b1c3c-...x-MS-Date:TUE, 03 Haz 2014 10:33:12 GMT.x-ms-version:2014-02-14./domemaildist/azuremmblobcontainer/blobCreated.txt. |
| de8b1c3c-... |Toowrite istek verileri hazırlanıyor. |
| e2d06d78-... |Yanıt bekleme sırasında özel durum oluştu: hello uzak sunucu bir hata döndürdü: (404) bulunamadı... |
| e2d06d78-... |Yanıtı alındı. Durum kodu 404, istek kimliği = 353ae3bc-..., Content-MD5 = =, ETag =. |
| e2d06d78-... |Yanıt Üstbilgileri hello hello işlemi kalanıyla etmeden başarıyla işlendi. |
| e2d06d78-... |Yanıt gövdesi yükleniyor. |
| e2d06d78-... |İşlem başarıyla tamamlandı. |
| e2d06d78-... |Zaman uyumsuz istek toohttps://domemaildist.blob.core.windows.net/azuremmblobcontainer başlatılıyor. |
| e2d06d78-... |StringToSign PUT =... 0...x-MS-Client-Request-id:e2d06d78-...x-MS-Date:TUE, 03 Haz 2014 10:33:12 GMT.x-ms-version:2014-02-14./domemaildist/azuremmblobcontainer.restype:container. |
| e2d06d78-... |Yanıtı bekleniyor. |
| de8b1c3c-... |Yazma isteği verileri. |
| de8b1c3c-... |Yanıtı bekleniyor. |
| e2d06d78-... |Yanıt bekleme sırasında özel durum oluştu: hello uzak sunucu bir hata döndürdü: (409) çakışma... |
| e2d06d78-... |Yanıtı alındı. Durum kodu 409, istek kimliği = c27da20e-..., Content-MD5 = =, ETag =. |
| e2d06d78-... |Hata yanıt gövdesi yükleniyor. |
| de8b1c3c-... |Yanıt bekleme sırasında özel durum oluştu: hello uzak sunucu bir hata döndürdü: (404) bulunamadı... |
| de8b1c3c-... |Yanıtı alındı. Durum kodu 404, istek kimliği = 0eaeab3e-..., Content-MD5 = =, ETag =. |
| de8b1c3c-... |Merhaba işlemi sırasında özel durum oluştu: hello uzak sunucu bir hata döndürdü: (404) bulunamadı... |
| de8b1c3c-... |Yeniden deneme ilkesi için bir yeniden deneme izin vermedi. Başarısız olan hello uzak sunucusu ile bir hata döndürdü: (404) bulunamadı... |
| e2d06d78-... |Yeniden deneme ilkesi için bir yeniden deneme izin vermedi. Başarısız olan hello uzak sunucusu ile bir hata döndürdü: (409) çakışma... |

Bu örnekte, hello istemci hello gelen istekleri Interleaving hello günlüğü gösterir, **CreateIfNotExists** hello hello isteklerinden (istek kimliği e2d06d78...) yöntemiyle **UploadFromStream** yöntemi ( de8b1c3c-...); Merhaba istemci uygulaması bu yöntemleri zaman uyumsuz olarak çağırma çünkü bu gerçekleştirilmektedir. Merhaba zaman uyumsuz hello istemci tooensure hello kapsayıcı tooupload denemeden önce tüm veri tooa blob bu kapsayıcıda oluşturur, kodda değiştirmeniz gerekir. İdeal olarak, tüm kapsayıcıları önceden oluşturmanız gerekir.

#### <a name="SAS-authorization-issue"></a>Bir paylaşılan erişim imzası (SAS) yetkilendirme sorunu
Merhaba istemci uygulaması toouse hello hello işlemi için gerekli izinleri içermez bir SAS anahtarı çalışırsa hello depolama hizmeti bir HTTP 404 (bulunamadı) ileti toohello istemci döndürür. Merhaba aynı zaman da görürsünüz için sıfır olmayan bir değer **SASAuthorizationError** hello ölçümleri içinde.

Aşağıdaki tablonun hello hello depolama günlüğü günlük dosyasından alınan örnek bir sunucu tarafı günlüğüne ileti gösterilir:

| Ad | Değer |
| --- | --- |
| İstek başlangıç zamanı | 2014-05-30T06:17:48.4473697Z |
| İşlem türü     | GetBlobProperties            |
| İstek durumu     | SASAuthorizationError        |
| HTTP durum kodu   | 404                          |
| Kimlik doğrulama türü| SAS                          |
| Hizmet türü       | Blob                         |
| İstek URL'si        | https://domemaildist.BLOB.Core.Windows.NET/azureimblobcontainer/blobCreatedViaSAS.txt |
| nbsp;              |   ? sv 2014-02-14 = & sr = c & si = mypolicy & SIG XXXXX =&;API sürümü 2014-02-14 = |
| İstek Kimliği üst bilgisi  | a1f348d5-8032-4912-93EF-b393e5252a3b |
| İstemci istek kimliği  | 2d064953-8436-4ee0-aa0c-65cb874f7929 |


İstemci uygulamanızı tooperform izinleri verilmemiş bir işlem neden deniyor araştırmanız gerekir.

#### <a name="JavaScript-code-does-not-have-permission"></a>İstemci tarafı JavaScript kodu izin tooaccess hello nesnesi yok
JavaScript istemci kullanıyorsanız ve hello depolama hizmeti HTTP 404 iletileri döndürüyor, aşağıdaki JavaScript hatalar hello tarayıcıda hello için denetleyin:

```
SEC7120: Origin http://localhost:56309 not found in Access-Control-Allow-Origin header.
SCRIPT7002: XMLHttpRequest: Network Error 0x80070005, Access is denied.
```

> [!NOTE]
> İstemci tarafı JavaScript sorunlarını giderirken hello tarayıcı ve hello depolama hizmeti arasında alınıp Internet Explorer tootrace hello iletileri hello F12 geliştirici araçlarını kullanabilirsiniz.
> 
> 

Merhaba web tarayıcısı hello uyguladığından bu hatalar ortaya [aynı kaynak İlkesi](http://www.w3.org/Security/wiki/Same_Origin_Policy) hello etki alanı hello sayfasından farklı bir etki alanındaki bir API'yi çağıran bir web sayfası engelleyen güvenlik kısıtlaması gelir.

toowork hello JavaScript sorunu çözmek Hello depolama hizmeti hello istemci erişimi için çapraz kaynak kaynak paylaşımı (CORS) yapılandırabilirsiniz. Daha fazla bilgi için bkz: [Azure Storage Hizmetleri için çıkış noktaları arası kaynak paylaşımı (CORS) Destek](http://msdn.microsoft.com/library/azure/dn535601.aspx).

Aşağıdaki kod örneği hello nasıl tooconfigure, blob hizmeti tooallow blob depolama hizmetinin bir blob'a hello Contoso etki alanı tooaccess çalıştıran JavaScript gösterir:

```csharp
CloudBlobClient client = new CloudBlobClient(blobEndpoint, new StorageCredentials(accountName, accountKey));
// Set hello service properties.
ServiceProperties sp = client.GetServiceProperties();
sp.DefaultServiceVersion = "2013-08-15";
CorsRule cr = new CorsRule();
cr.AllowedHeaders.Add("*");
cr.AllowedMethods = CorsHttpMethods.Get | CorsHttpMethods.Put;
cr.AllowedOrigins.Add("http://www.contoso.com");
cr.ExposedHeaders.Add("x-ms-*");
cr.MaxAgeInSeconds = 5;
sp.Cors.CorsRules.Clear();
sp.Cors.CorsRules.Add(cr);
client.SetServiceProperties(sp);
```

#### <a name="network-failure"></a>Ağ hatası
Bazı durumlarda, kayıp ağ paketlerini HTTP 404 iletileri toohello istemci döndürme toohello depolama birimi hizmeti yol açabilir. Örneğin, istemci uygulamanız hello tablo hizmetinden bir varlık silinirken bir depolama özel durumu raporlama throw hello istemci bkz bir "HTTP 404 (bulunamadı)" Merhaba tablo hizmetinden gelen durum iletisi. Merhaba tablo depolama hizmeti hello tabloda incelediğinizde hello hizmet istendiği gibi hello varlık sildi bakın.

Merhaba İstemcisi'nde Hello özel durum ayrıntıları dahil hello isteği için hello tablo hizmeti tarafından atanan hello istek kimliği (7e84f12d...): hello arayarak bu bilgileri toolocate hello İstek Ayrıntıları hello sunucu tarafı depolama günlüklerindeki kullanabilir  **istek kimliği üstbilgisi** hello günlük dosyasında sütun. Bu hata gibi bu oluşur ve hello zaman hello ölçümleri temel hello günlük dosyalarını aramak hataları kaydedilirken hello ölçümleri tooidentify de kullanabilirsiniz. Delete hello bu günlük girişi gösterir bir "HTTP (404) istemci başka bir hata" durum iletisi ile başarısız oldu. Merhaba aynı günlük girişi da hello hello istemci tarafından oluşturulan hello istek kimliğini içerir **istemci istek kimliği** sütun (813ea74f...).

Hello sunucu tarafı günlük da hello ile başka bir giriş içerir aynı **istemci istek kimliği** değeri (813ea74f...) başarılı bir silme işlemi için hello aynı varlık ve gelen aynı hello istemci. Bu başarılı silme işlemi hello başarısız silme isteği çok kısa bir süre önce yapıldı.

Merhaba en olası nedeni, bu senaryo, başarılı oldu, ancak onay (belki de son tooa geçici ağ sorunu) hello sunucusundan almadı hello varlık toohello tablo hizmeti için bir silme isteği gönderilen bu hello istemcidir. Merhaba istemci ardından hello işlemi otomatik olarak yeniden (kullanarak, hello aynı **istemci istek kimliği**), bu yeniden deneme hello varlık zaten silinmiş olduğundan başarısız oldu.

Bu sorun sık sık olursa hello istemci tooreceive onayları hello tablo hizmetinden neden başarısız araştırmanız gerekir. Merhaba zaman zaman ortaya çıkan bir sorundur, hello "HTTP (404) bulunamadı" hatasını yakalamak ve hello istemcisinde oturum ancak hello istemci toocontinue izin.

### <a name="the-client-is-receiving-409-messages"></a>Merhaba istemci HTTP 409 (Çakışma) iletileri alma
Merhaba aşağıdaki tabloda gösterilmektedir iki istemci işlemleri hello sunucu tarafı günlüğünden bir Ayıkla: **DeleteIfExists** göre hemen ardından **CreateIfNotExists** kullanarak hello aynı blob kapsayıcı adı. Her istemci işlemi gönderilen iki istekleri toohello Server'da ilk sonuçları Not bir **GetContainerProperties** isteği toocheck hello kapsayıcının var olduğunun hello tarafından izlenen **DeleteContainer** veya  **CreateContainer** isteği.

| zaman damgası | İşlem | Sonuç | Kapsayıcı adı | İstemci istek kimliği |
| --- | --- | --- | --- | --- |
| 05:10:13.7167225 |GetContainerProperties |200 |mmcont |c9f52c89-... |
| 05:10:13.8167325 |DeleteContainer |202 |mmcont |c9f52c89-... |
| 05:10:13.8987407 |GetContainerProperties |404 |mmcont |bc881924-... |
| 05:10:14.2147723 |CreateContainer |409 |mmcont |bc881924-... |

Merhaba hello istemci uygulamasındaki kod siler ve sonra hemen hello kullanarak bir blob kapsayıcısını yeniden oluşturur aynı adı: Merhaba **CreateIfNotExists** yöntemi (istemci istek kimliği bc881924-...) sonunda hello HTTP 409 (Çakışma) ile başarısız oluyor bir hata oluştu. Bir istemci blob kapsayıcılar, tablolar veya kısa bir süre önce yoktur sıraları sildiğinde hello adı yeniden kullanılabilir hale gelir.

Merhaba silme/yeniden oluşturun düzeni ortak ise yeni kapsayıcılar oluşturduğunda Merhaba istemci uygulaması benzersiz kapsayıcı adları kullanmanız gerekir.

### <a name="metrics-show-low-percent-success"></a>Düşük PercentSuccess ölçümleri göster veya ClientOtherErrors işlem durumundaki işlemlerini analytics günlük girdilerine sahip
Merhaba **PercentSuccess** ölçüm hello yüzde başarılı oldu, HTTP durum kodu göre işlemlerinin yakalar. Durum kodları işlemleriyle 2XX, durum kodları 3XX, 4XX ve 5XX aralıklardaki işlemleriyle başarısız ve alt hello sayılır ancak olarak başarılı Say **PercentSucess** ölçüm değeri. Merhaba sunucu tarafı depolama günlük dosyalarında bir işlem durumuyla işlemlerini kaydedilir **ClientOtherErrors**.

Bu işlemleri tamamladınız ve bu nedenle kullanılabilirliği gibi diğer ölçümleri etkilemez önemli toonote olur. Başarıyla yürütülen ancak başarısız HTTP durum kodları sonuçlanabilir işlemlerinin bazı örnekler şunlardır:

* **ResourceNotFound** (değil bulunan 404), örneğin bir GET isteği tooa blob yok.
* **ResouceAlreadyExists** (409 çakışma), örneğin bir **CreateIfNotExist** burada hello kaynak zaten var. işlemi.
* **ConditionNotMet** (değil değiştiren 304), bir istemci gönderdiğinde gibi örneğin bir koşullu işlem bir **ETag** değeri ve bir HTTP **If-None-Match** üstbilgi toorequest bir görüntü yalnızca if Merhaba son işlem güncelleştirildi.

Merhaba depolama hizmetleri hello sayfasına dönmek ortak REST API hata kodları listesini bulabilirsiniz [ortak REST API hata kodları](http://msdn.microsoft.com/library/azure/dd179357.aspx).

### <a name="capacity-metrics-show-an-unexpected-increase"></a>Kapasite ölçümlerini beklenmeyen artışı depolama kapasitesi kullanımı Göster
Kapasite kullanımı depolama hesabınızdaki beklenmeyen değişiklikleri ani görürseniz, kullanılabilirlik ölçümlerinizi bakarak hello nedenleri araştırabilirsiniz; Örneğin, bir artış hello başarısız silme isteklerinin sayısı tooan artış uygulama belirli temizleme işlemleri toobe alan boşaltıp (için beklendiği gibi çalışmıyor olabilir beklenen olarak kullandığınız blob storage'nın hello tutardaki neden olabilir örnek, alan boşaltıp için kullanılan hello SAS belirteci süresi dolduğundan).

### <a name="you-are-experiencing-unexpected-reboots"></a>Beklenmeyen yeniden başlatmalar çok sayıda ekli VHD'ler sahip Azure sanal makineleri yaşıyor
Bir Azure sanal makine (VM) çok sayıda hello olan ekli VHD'ler varsa aynı depolama hesabını hello ölçeklenebilirlik hedefleri hello VM toofail neden bir depolama hesabı için aşan. Merhaba dakika ölçümleri hello depolama hesabı için denetlemeniz gerekir (**TotalRequests**/**Totalıngress**/**TotalEgress**) ani için bir depolama hesabı için hello ölçeklenebilirlik hedefleri aşıyor. Merhaba bölümüne bakın "[ölçümleri Göster artışı içinde PercentThrottlingError]" azaltma belirlenmesinde yardım depolama hesabınıza oluştu için.

Genel olarak, her tek tek giriş veya çıkış işlemi bir sanal makineden bir VHD çok çevirir**Al sayfasında** veya **Put sayfa** sayfa blobu temel hello işlemleri. Bu nedenle, kullanabileceğiniz hello tahmini IOPS, ortam tootune için kaç tane VHD'ler, tek bir depolama hesabında dayalı hello belirli bir davranışı, uygulamanızın üzerinde. Tek bir depolama hesabında birden fazla 40 disklere sahip önermiyoruz. Bkz: [Azure Storage ölçeklenebilirlik ve performans hedefleri](storage-scalability-targets.md) depolama hesapları için geçerli ölçeklenebilirlik hedefleri hello Ayrıntılar için özellikle hello toplam istek oranı ve toplam bant genişliği hello türde depolama hesabı için kullandığınız .
Depolama hesabınız için hello ölçeklenebilirlik hedefleri aşan gerekirse, birden çok farklı depolama hesapları tooreduce hello etkinliğinde ayrı ayrı her hesap Vhd'lerinizi yerleştirmeniz.

### <a name="your-issue-arises-from-using-the-storage-emulator"></a>Sorununuzu geliştirme veya test için hello storage öykünücüsü kullanarak ortaya çıkar.
Genellikle geliştirme sırasında hello storage öykünücüsünü kullanma ve bir Azure depolama hesabı için tooavoid hello gereksinimi sınayın. Merhaba depolama öykünücüsü kullanırken oluşabilecek hello sık karşılaşılan sorunları şunlardır:

* [Özellik "X" Merhaba depolama öykünücüsünde çalışmıyor]
* [Hata "Merhaba HTTP üst bilgilerinden biri için hello değer hello doğru biçimde değil" ne zaman kullanarak izin ver hello depolama öykünücüsü]
* [Çalışan hello depolama öykünücüsü yönetici ayrıcalıkları gerektirir]

#### <a name="feature-X-is-not-working"></a>Özellik "X" Merhaba depolama öykünücüsünde çalışmıyor
Merhaba depolama öykünücüsü tüm hello dosya hizmeti gibi hello Azure depolama hizmetleri hello özelliklerini desteklemez. Daha fazla bilgi için bkz: [kullanım hello geliştirme ve sınama için Azure Storage öykünücüsü](storage-use-emulator.md).

Depolama hello bu özellikleri için öykünücüsü yok desteği, hello Azure depolama hizmeti hello bulutta kullanın.

#### <a name="error-HTTP-header-not-correct-format"></a>Hata "Merhaba HTTP üst bilgilerinden biri için hello değer hello doğru biçimde değil" ne zaman kullanarak izin ver hello depolama öykünücüsü
Merhaba yerel depolama öykünücüsü ve yöntem çağrıları karşı hello depolama istemci kitaplığı gibi kullanan uygulamanızı test **CreateIfNotExists** hello hatasıyla başarısız iletisi "Merhaba değeri hello HTTP üst bilgilerinden biri içinde değil Merhaba doğru biçimi." Bu, hello gösterir kullanmakta olduğunuz hello depolama öykünücüsü sürümüne kullanmakta olduğunuz hello depolama istemci kitaplığı hello sürümünü desteklemiyor. Merhaba depolama istemci kitaplığı hello üstbilgisi ekler **x-ms-version** tooall hello istekleri kolaylaştırır. Merhaba depolama öykünücüsü hello hello değerinde tanımıyor varsa **x-ms-version** başlık hello isteği reddeder.

Merhaba depolama kitaplık istemcisi günlükleri toosee hello değeri hello kullanabilirsiniz **x-ms-version üstbilgi** onu gönderiyor. Merhaba hello değerini de görebilirsiniz **x-ms-version üstbilgi** Fiddler tootrace hello istekleri, istemci uygulamasından kullanıyorsanız.

Bu senaryo genellikle yüklemek ve hello depolama öykünücüsü güncelleştirmeden hello hello depolama istemci kitaplığı en son sürümünü kullanmanız halinde oluşur. , Hello hello depolama öykünücüsü en son sürümünü yükleyin veya Bulut depolama hello öykünücüsü yerine geliştirme ve test için kullanmak.

#### <a name="storage-emulator-requires-administrative-privileges"></a>Çalışan hello depolama öykünücüsü yönetici ayrıcalıkları gerektirir
Merhaba depolama öykünücüsü çalıştırdığınızda, yönetici kimlik bilgileri istenir. Bu, yalnızca ilk kez hello için hello depolama öykünücüsü başlatırken oluşur. Merhaba depolama öykünücüsü ayarladıktan sonra yönetici ayrıcalıkları toorun gerekmez tekrar.

Daha fazla bilgi için bkz: [kullanım hello geliştirme ve sınama için Azure Storage öykünücüsü](storage-use-emulator.md). Ayrıca yönetici ayrıcalıkları gerektirir Visual Studio hello depolama öykünücüsünde da başlatabilir unutmayın.

### <a name="you-are-encountering-problems-installing-the-Windows-Azure-SDK"></a>.NET için Azure SDK'sı hello yüklerken sorunlarla karşılaşıyoruz
Tooinstall hello SDK çalıştığınızda, yerel makinenizde çalışırken tooinstall hello depolama öykünücüsü başarısız olur. Merhaba yükleme günlüğü iletileri aşağıdaki hello birini içerir:

* CAQuietExec: Hata: oluşturulamıyor tooaccess SQL örneği
* CAQuietExec: Hata: oluşturulamıyor toocreate veritabanı

Merhaba, var olan LocalDB yükleme ile ilgili bir sorunu nedenidir. Hello Azure storage Hizmetleri benzetim varsayılan olarak, yerel veritabanı toopersist veri hello depolama öykünücüsü kullanır. Bir komut istemi penceresindeki komutları tooinstall hello SDK denemeden önce aşağıdaki hello çalıştırarak LocalDB örneğinizi sıfırlayabilirsiniz.

```
sqllocaldb stop v11.0
sqllocaldb delete v11.0
delete %USERPROFILE%\WAStorageEmulatorDb3*.*
sqllocaldb create v11.0
```

Merhaba **silmek** komutu, önceki hello depolama öykünücüsü yüklemelerinden eski tüm veritabanı dosyaları kaldırır.

### <a name="you-have-a-different-issue-with-a-storage-service"></a>Bir depolama hizmetindeki farklı bir sorun olması
Merhaba önceki sorun giderme bölümleri olan bir depolama hizmeti yaşıyor hello sorunu eklemezseniz yaklaşım toodiagnosing izleyerek ve sorununuzu gidermeye hello benimsemeyi.

* Beklenen taban çizgisinin davranış gelen herhangi bir değişiklik varsa, ölçümleri toosee denetleyin. Merhaba ölçümleri, geçici veya kalıcı hello sorundur ve sorunun hangi depolama işlemleri hello etkileyen olup olmadığını mümkün toodetermine olabilir.
* Toohelp oluşan hatalar hakkında daha ayrıntılı bilgi için sunucu tarafı günlük verileri arama hello ölçümleri bilgileri kullanabilirsiniz. Bu bilgiler, sorun giderme ve hello sorunu çözmenize yardımcı olabilir.
* Merhaba sunucu tarafı günlüklerindeki Hello bilgi yeterli tootroubleshoot hello sorunu başarılı olmazsa, hello depolama istemci kitaplığı istemci tarafı günlüklerini tooinvestigate hello davranışını istemci uygulaması ve Fiddler, Wireshark gibi araçları kullanabilirsiniz, ve Microsoft Message Analyzer tooinvestigate ağınıza.

Fiddler'ı kullanma hakkında daha fazla bilgi için bkz: "[ek 1: Fiddler toocapture HTTP ve HTTPS trafiği kullanılarak]."

Wireshark kullanma hakkında daha fazla bilgi için bkz: "[ek 2: Wireshark toocapture ağ trafiğini kullanarak]."

Microsoft Message Analyzer kullanma hakkında daha fazla bilgi için bkz: "[ek 3: Microsoft Message Analyzer toocapture ağ trafiğini kullanarak]."

## <a name="appendices"></a>Ekler
Merhaba ekler, tanılama ve Azure Storage (ve diğer hizmetleri) ile ilgili sorunları giderme zaman yararlı bulabilirsiniz çeşitli araçlar açıklanmaktadır. Bu araçları Azure Storage parçası olmayan ve üçüncü taraf ürünleri bazılarıdır. Bu nedenle, bu eklerin ele alınan hello araçları tarafından Microsoft Azure veya Azure Storage yaptığınız herhangi bir destek sözleşmesi kapsamında değildir ve değerlendirme işleminizin bir parçası olarak bu nedenle hello lisans ve Destek seçeneklerini kullanılabilir incelemeniz gerekir Bu araçların Hello sağlayıcıları.

### <a name="appendix-1"></a>Ek 1: Fiddler toocapture HTTP ve HTTPS trafiğini kullanma
[Fiddler](http://www.telerik.com/fiddler) istemci uygulaması ve hello kullanmakta olduğunuz Azure depolama hizmeti arasındaki hello HTTP ve HTTPS trafiği çözümleme için yararlı bir araçtır.

> [!NOTE]
> Fiddler HTTPS trafiği kod çözme; Merhaba Fiddler belgelerini dikkatle okumalıdır toounderstand nasıl bunu yapar ve toounderstand hello güvenlik kapsamı.
> 
> 

Bu ekte nasıl tooconfigure Fiddler toocapture trafiği arasında hello yerel makine nerede fiddler'ı yüklemiş ve Azure storage Hizmetleri hello izlenecek ile ilgili kısa bir yol sağlar.

Fiddler başlatıldıktan sonra HTTP ve HTTPS trafiği yerel makinenizde yakalama başlar. Merhaba, Fiddler denetlemek için bazı yararlı komutlar şunlardır:

* Durdurun ve trafiği yakalama başlatın. Merhaba ana menüde çok Git**dosya** ve ardından **trafiği Yakala** tootoggle açma ve kapatma yakalama.
* Yakalanan trafik verileri kaydedin. Merhaba ana menüde çok Git**dosya**, tıklatın **kaydetmek**ve ardından **tüm oturumları**: Bu oturumu arşiv dosyasında toosave hello trafiğini etkinleştirir. Bir oturum arşiv çözümleme için daha sonra yeniden yükleyin veya tooMicrosoft destek istediyseniz gönderin.

Fiddler yakalar trafik toolimit hello miktarı, hello yapılandırma filtreleri kullanabilir **filtreleri** ekran aşağıdaki sekmesini hello gösterir yalnızca gönderilen trafiğin toohello yakalayan bir filtre  **contosoemaildist.Table.Core.Windows.NET** depolama uç noktası:

![][5]

### <a name="appendix-2"></a>Ek 2: Wireshark toocapture ağ trafiğini kullanma
[Wireshark](http://www.wireshark.org/) tooview sağlayan bir ağ protokolü Çözümleyicisi paket için ayrıntılı bilginin çok çeşitli ağ protokolleri.

Merhaba aşağıdaki yordamda nasıl toocapture paket için hello yerel makine trafiğinden ayrıntılı bilgileri Azure depolama hesabınızdaki Wireshark toohello tablo hizmeti yüklü olduğu gösterilmektedir.

1. Wireshark yerel makinenizde başlatın.
2. Merhaba, **Başlat** bölümü, select hello yerel ağ arabirim veya bağlı toohello olan arabirimler Internet.
3. Tıklatın **yakalama seçenekleri**.
4. Bir filtre toohello ekleme **yakalama filtresi** metin kutusu. Örneğin, **contosoemaildist.table.core.windows.net konak** paketleri hello tablo Hizmeti uç noktası hello içinde tooor gönderildiği yalnızca Wireshark toocapture yapılandıracak **contosoemaildist** depolama hesabı. Merhaba denetleyin [yakalama filtreleri tam listesi](http://wiki.wireshark.org/CaptureFilters).
   
   ![][6]
5. Tıklatın **Başlat**. İstemci uygulamanızı yerel makinenizde kullandıkça Wireshark şimdi tüm hello paketleri gönderme tooor hello tablo Hizmeti uç noktasından yakalar.
6. Tamamladığınızda, hello ana menü çubuğunda **yakalama** ve ardından **durdurmak**.
7. toosave hello yakalanan veri dosyasındaki Wireshark yakalama üzerinde hello ana menü öğesini **dosya** ve ardından **kaydetmek**.

WireShark hello mevcut herhangi bir hata vurgulayın **packetlist** penceresi. Merhaba de kullanabilirsiniz **Uzman bilgilerini** penceresi (tıklatın **Çözümle**, ardından **Uzman bilgilerini**) tooview hataların ve uyarıların özetini.

![][7]

Ayrıca seçebilirsiniz tooview hello TCP veri TCP veri hello üzerinde sağ tıklayıp seçerek hello uygulama katmanı tarafından görülen şekilde **izleyin TCP akışı**. Yakalama Filtresi olmadan, döküm yakalanmış durumunda bu özellikle yararlıdır. Daha fazla bilgi için bkz: [TCP akışları aşağıdaki](http://www.wireshark.org/docs/wsug_html_chunked/ChAdvFollowTCPSection.html).

![][8]

> [!NOTE]
> Merhaba Wireshark kullanma hakkında daha fazla bilgi için bkz: [Wireshark Kullanıcı Kılavuzu](http://www.wireshark.org/docs/wsug_html_chunked).
> 
> 

### <a name="appendix-3"></a>Ek 3: Microsoft Message Analyzer toocapture ağ trafiğini kullanma
Microsoft Message Analyzer toocapture HTTP ve HTTPS trafiğinin bir benzer şekilde tooFiddler kullanın ve benzer bir şekilde tooWireshark'nde ağ trafiği yakalayın.

#### <a name="configure-a-web-tracing-session-using-microsoft-message-analyzer"></a>Microsoft Message Analyzer kullanarak bir web izleme oturumu yapılandırın
bir web izleme oturumu hello Microsoft Message Analyzer uygulamayı çalıştırın, Microsoft Message Analyzer kullanarak HTTP ve HTTPS trafiği için ve ardından hello tooconfigure **dosya** menüsünde tıklatın **yakalama/izleme**. Kullanılabilir izleme senaryoları Hello listesinde seçin **Web Proxy**. Merhaba sonra **izleme senaryo Yapılandırması** panelinde hello **HostnameFilter** metin kutusuna, depolama noktalarınızı hello adlarını ekleyin (Bu hello adlarında arayabilir [Azure portal](https://portal.azure.com)). Örneğin, hello Azure depolama hesabınızın adını ise **contosodata**, toohello aşağıdaki hello eklemelisiniz **HostnameFilter** textbox:

```
contosodata.blob.core.windows.net contosodata.table.core.windows.net contosodata.queue.core.windows.net
```

> [!NOTE]
> Bir boşluk karakteri hello ana bilgisayar adları ayırır.
> 
> 

İzleme verilerini toplama hazır toostart olduğunda hello tıklatın **Başlat ile** düğmesi.

Merhaba Microsoft Message Analyzer hakkında daha fazla bilgi için **Web Proxy** izlemek için bkz: [Microsoft PEF WebProxy sağlayıcısı](http://technet.microsoft.com/library/jj674814.aspx).

Merhaba yerleşik **Web Proxy** Microsoft Message Analyzer içinde izleme Fiddler üzerinde temel; istemci-tarafı HTTPS trafiği yakalayabilir ve şifrelenmemiş HTTPS iletileri görüntüler. Merhaba **Web Proxy** izleme works erişim toounencrypted iletileri verir tüm HTTP ve HTTPS trafiği için yerel bir ara yapılandırarak.

#### <a name="diagnosing-network-issues-using-microsoft-message-analyzer"></a>Microsoft Message Analyzer kullanarak ağ sorunlarını tanılama
Ayrıca toousing hello Microsoft Message Analyzer **Web Proxy** izleme toocapture ayrıntılarını Merhaba istemci uygulaması ve hello depolama hizmeti arasında HTTP/HTTPs trafiğini Merhaba, hello yerleşik de kullanabilirsiniz  **Yerel bağlantı katmanı** izleme toocapture ağ paket bilgileri. Bırakılan paketleri ile Wireshark yakalamak ve Tanılama, toocapture veri benzer toothat ağ sorunları gibi bu etkinleştirir.

Merhaba aşağıdaki ekran görüntüsünde gösteren bir örnek **yerel bağlantı katmanı** bazı izleme **bilgilendirme** hello iletilerinde **DiagnosisTypes** sütun. Merhaba bir simgeyi tıklatarak **DiagnosisTypes** sütun selamlama iletisine hello ayrıntılarını gösterir. Bu örnekte, hello sunucu ileti #305 yeniden aktarılan, bu onay hello istemciden almadığı için:

![][9]

Microsoft Message Analyzer hello izleme oturumu oluşturduğunuzda hello izlemede filtreleri tooreduce hello parazit miktarını belirtebilirsiniz. Merhaba üzerinde **yakalama / izleme** hello izleme tanımladığınız yerlerde sayfasını tıklatın hello üzerinde **yapılandırma** sonraki çok bağlantı**Microsoft-Windows-NDIS-PacketCapture**. Ekran aşağıdaki hello TCP trafiği hello IP adreslerini üç depolama hizmetleri için filtreler bir yapılandırması gösterilmektedir:

![][10]

Merhaba Microsoft Message Analyzer yerel bağlantı katmanı izleme hakkında daha fazla bilgi için bkz: [PEF NDIS PacketCapture Microsoft sağlayıcısı](http://technet.microsoft.com/library/jj659264.aspx).

### <a name="appendix-4"></a>Ek 4: Excel kullanarak tooview ölçümleri ve günlük verileri
Birçok araçları kolay tooload hello veri için Excel'e görüntüleme kolaylaştırır sınırlandırılmış biçimi ve analiz Azure tablo depolama biriminden toodownload hello Storage ölçümleri verileri sağlar. Excel'e yükleyebilir sınırlandırılmış biçimde depolama günlük verileri Azure blob depolama biriminden zaten var. Ancak, hello bilgilerine dayalı tooadd uygun sütun başlıkları gerekir [depolama Analytics günlük biçimi](http://msdn.microsoft.com/library/azure/hh343259.aspx) ve [Storage Analytics Ölçüm tablosu şeması](http://msdn.microsoft.com/library/azure/hh343264.aspx).

tooimport blob depolama alanından, depolama günlüğü verileri Excel'e çalıştırdıktan sonra yükleyin:

* Merhaba üzerinde **veri** menüsünde tıklatın **metindeki**.
* Tooview istediğiniz Gözat toohello günlük dosyası **alma**.
* Üzerinde hello 1. adımda **Metin Alma Sihirbazı**seçin **sınırlandırılmış**.

Üzerinde hello 1. adımda **Metin Alma Sihirbazı**seçin **noktalı** olarak yalnızca sınırlayıcı hello ve çift tırnaklı hello olarak seçin **Metin niteleyicisi**. Ardından **son** ve burada tooplace hello kitabınızdaki verilere'i seçin.

### <a name="appendix-5"></a>Ek 5: Visual Studio Team Services için Application Insights ile izleme
Ayrıca, Visual Studio Team Services için performans ve kullanılabilirlik izlemesi parçası olarak hello Application Insights özelliğini kullanabilirsiniz. Bu araç şunları yapabilir:

* Web hizmetiniz kullanılabilir ve yanıt verebilir durumda olduğundan emin olun. Uygulamanızı bir web sitesi veya web hizmeti kullanan bir cihaz uygulaması olsun, bu Merhaba Dünya konumlardan birkaç dakikada URL'nizi sınamak ve bir sorun olup olmadığını size bildirmek.
* Hızlı bir şekilde herhangi bir performans sorunları veya web hizmetiniz durumlar tanılayın. CPU veya diğer kaynakları uzatılır değilse, özel durumlar Yığın izlemeleri edinin öğrenmek ve günlük izlemelerini kolayca arayın. Merhaba, uygulamanın performansını yaşanması kabul edilebilir sınırlar aşağıda size gönderebilir, bir e-posta. .NET ve Java web Hizmetleri'ni izleyebilirsiniz.

Daha fazla bilgi bulabilirsiniz [Application Insights nedir?](../application-insights/app-insights-overview.md).

<!--Anchors-->
[Giriş]: #introduction
[Bu kılavuz nasıl düzenlenir]: #how-this-guide-is-organized

[, depolama hizmet izlemesini]: #monitoring-your-storage-service
[Hizmet durumu izleme]: #monitoring-service-health
[Kapasite izleme]: #monitoring-capacity
[Kullanılabilirlik izlemesi]: #monitoring-availability
[Performans izleme]: #monitoring-performance

[depolama sorunları tanılama]: #diagnosing-storage-issues
[Hizmet sistem durumu sorunları]: #service-health-issues
[Performans sorunları]: #performance-issues
[Hatalarını tanılama]: #diagnosing-errors
[Depolama öykünücüsü sorunları]: #storage-emulator-issues
[Depolama günlük araçları]: #storage-logging-tools
[Ağ günlük araçlarını kullanarak]: #using-network-logging-tools

[uçtan uca izleme]: #end-to-end-tracing
[Günlük verileri ilişkilendirme]: #correlating-log-data
[İstemci istek kimliği]: #client-request-id
[sunucu istek kimliği]: #server-request-id
[Zaman damgaları]: #timestamps

[sorun giderme kılavuzluğu]: #troubleshooting-guidance
[ölçümleri Göster yüksek AverageE2ELatency ve düşük AverageServerLatency]: #metrics-show-high-AverageE2ELatency-and-low-AverageServerLatency
[Düşük AverageE2ELatency ve düşük AverageServerLatency ölçümleri göster ancak hello istemci yüksek gecikme yaşanıyor]: #metrics-show-low-AverageE2ELatency-and-low-AverageServerLatency
[Ölçümler yüksek AverageServerLatency gösteriyor]: #metrics-show-high-AverageServerLatency
[Kuyrukta ileti tesliminde beklenmeyen gecikmeler yaşıyorsunuz]: #you-are-experiencing-unexpected-delays-in-message-delivery

[ölçümleri Göster artışı içinde PercentThrottlingError]: #metrics-show-an-increase-in-PercentThrottlingError
[PercentThrottlingError geçici artış]: #transient-increase-in-PercentThrottlingError
[PercentThrottlingError hata kalıcı artış]: #permanent-increase-in-PercentThrottlingError
[ölçümleri Göster artışı içinde PercentTimeoutError]: #metrics-show-an-increase-in-PercentTimeoutError
[Ölçümler PercentNetworkError’da artış gösteriyor]: #metrics-show-an-increase-in-PercentNetworkError

[Merhaba istemci HTTP 403 (Yasak) iletileri alma]: #the-client-is-receiving-403-messages
[Merhaba istemci HTTP 404 (bulunamadı) iletileri alma]: #the-client-is-receiving-404-messages
[Merhaba istemci veya başka bir işlem daha önce silinmiş hello nesnesi]: #client-previously-deleted-the-object
[Bir paylaşılan erişim imzası (SAS) yetkilendirme sorunu]: #SAS-authorization-issue
[İstemci tarafı JavaScript kodu izin tooaccess hello nesnesi yok]: #JavaScript-code-does-not-have-permission
[Ağ hatası]: #network-failure
[Merhaba istemci HTTP 409 (Çakışma) iletileri alma]: #the-client-is-receiving-409-messages

[ölçümleri Göster düşük PercentSuccess veya analytics günlük girişlerini sahip işlemler işlem durumu ClientOtherErrors]: #metrics-show-low-percent-success
[Kapasite ölçümlerini beklenmeyen artışı depolama kapasitesi kullanımı Göster]: #capacity-metrics-show-an-unexpected-increase
[Çok sayıda ekli VHD'ler sahip sanal makinelerin beklenmeyen yeniden başlatmalar yaşıyor]: #you-are-experiencing-unexpected-reboots
[Sorununuzu geliştirme veya test için hello storage öykünücüsü kullanarak ortaya çıkar.]: #your-issue-arises-from-using-the-storage-emulator
[Özellik "X" Merhaba depolama öykünücüsünde çalışmıyor]: #feature-X-is-not-working
[Hata "Merhaba HTTP üst bilgilerinden biri için hello değer hello doğru biçimde değil" ne zaman kullanarak izin ver hello depolama öykünücüsü]: #error-HTTP-header-not-correct-format
[Çalışan hello depolama öykünücüsü yönetici ayrıcalıkları gerektirir]: #storage-emulator-requires-administrative-privileges
[.NET için Azure SDK'sı hello yüklerken sorunlarla karşılaşıyoruz]: #you-are-encountering-problems-installing-the-Windows-Azure-SDK
[Bir depolama hizmetindeki farklı bir sorun olması]: #you-have-a-different-issue-with-a-storage-service

[ekler]: #appendices
[ek 1: Fiddler toocapture HTTP ve HTTPS trafiği kullanılarak]: #appendix-1
[ek 2: Wireshark toocapture ağ trafiğini kullanarak]: #appendix-2
[ek 3: Microsoft Message Analyzer toocapture ağ trafiğini kullanarak]: #appendix-3
[Ek 4: Excel kullanarak tooview ölçümleri ve günlük verileri]: #appendix-4
[Ek 5: Visual Studio Team Services için Application Insights ile izleme]: #appendix-5

<!--Image references-->
[1]: ./media/storage-monitoring-diagnosing-troubleshooting/overview.png
[3]: ./media/storage-monitoring-diagnosing-troubleshooting/hour-minute-metrics.png
[4]: ./media/storage-monitoring-diagnosing-troubleshooting/high-e2e-latency.png
[5]: ./media/storage-monitoring-diagnosing-troubleshooting/fiddler-screenshot.png
[6]: ./media/storage-monitoring-diagnosing-troubleshooting/wireshark-screenshot-1.png
[7]: ./media/storage-monitoring-diagnosing-troubleshooting/wireshark-screenshot-2.png
[8]: ./media/storage-monitoring-diagnosing-troubleshooting/wireshark-screenshot-3.png
[9]: ./media/storage-monitoring-diagnosing-troubleshooting/mma-screenshot-1.png
[10]: ./media/storage-monitoring-diagnosing-troubleshooting/mma-screenshot-2.png
