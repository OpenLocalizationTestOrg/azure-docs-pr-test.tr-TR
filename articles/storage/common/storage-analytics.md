---
title: "Azure Storage Analytics toocollect günlüklerini ve ölçümleri veri aaaUse | Microsoft Docs"
description: "Storage Analytics tootrack ölçüm verilerini tüm depolama hizmetleri sağlar ve toocollect Blob, kuyruk ve tablo depolama için günlüğe kaydeder."
services: storage
documentationcenter: 
author: robinsh
manager: timlt
editor: tysonn
ms.assetid: 7894993b-ca42-4125-8f17-8f6dfe3dca76
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 03/03/2017
ms.author: robinsh
ms.openlocfilehash: aba1a236cb69fa2e60bcb8fda5d34841e36e379a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="storage-analytics"></a>Depolama Analizi

Azure Depolama Analizi günlük kaydı yapar ve depolama hesabı için ölçüm verileri sağlar. Bu veri tootrace istekleri kullanır, kullanım eğilimleri çözümlemek ve depolama hesabınızla sorunlarını tanılamak.

Storage Analytics toouse etkinleştirmeniz gerekir, tek tek her hizmet için toomonitor istediğiniz. Hello etkinleştirmek [Azure Portal](https://portal.azure.com). Ayrıntılar için bkz [hello Azure Portal'da depolama hesabı izleme](storage-monitor-storage-account.md). Storage Analytics hello REST API aracılığıyla programlı olarak veya hello istemci kitaplığı da etkinleştirebilirsiniz. Kullanım hello [Blob hizmeti özellik alma](https://msdn.microsoft.com/library/hh452239.aspx), [sıra hizmeti özelliklerini alma](https://msdn.microsoft.com/library/hh452243.aspx), [tablo hizmeti özellik alma](https://msdn.microsoft.com/library/hh452238.aspx), ve [dosya hizmeti özellikleriAl](https://msdn.microsoft.com/library/mt427369.aspx) her hizmet için işlemleri tooenable depolama çözümlemeleri.

Merhaba toplanan veriler (günlük için) iyi bilinen bir blob ve hello Blob hizmeti ve tablo hizmeti API'leri kullanılarak erişilebilecek (için ölçümleri), iyi bilinen tablolara depolanır.

Storage Analytics bir 20 TB'ye hello depolama hesabınız için toplam sınırı hello bağımsızdır depolanan veri miktarına sahiptir. Faturalama ve veri bekletme ilkeleri hakkında daha fazla bilgi için bkz: [depolama çözümlemeleri ve faturalama](https://msdn.microsoft.com/library/hh360997.aspx). Depolama hesabı sınırları hakkında daha fazla bilgi için bkz: [Azure Storage ölçeklenebilirlik ve performans hedefleri](storage-scalability-targets.md).

Kapsamlı bir kılavuz depolama çözümlemeleri ve diğer araçları tooidentify kullanma hakkında bilgi için tanılama ve Azure Storage ile ilgili sorunları giderme bkz [izleme, tanılama ve Microsoft Azure Storage sorun giderme](storage-monitoring-diagnosing-troubleshooting.md).

## <a name="about-storage-analytics-logging"></a>Storage Analytics oturum açma hakkında
Storage Analytics başarılı ve başarısız istekleri tooa depolama birimi hizmeti hakkındaki ayrıntılı bilgileri kaydeder. Bu bilgiler kullanılan toomonitor istekleri ayrı ayrı ve depolama hizmeti toodiagnose sorunları olabilir. İstekleri en iyi çaba ilkesine göre günlüğe kaydedilir.

Yalnızca depolama hizmeti etkinliği ise günlük girişleri oluşturulur. Örneğin, bir depolama hesabı Blob hizmeti ancak tablo veya kuyruğu hizmetlerinin etkinlik varsa, yalnızca toohello Blob hizmeti ilgili günlükleri oluşturulur.

Storage Analytics günlüğü Azure File storage için kullanılabilir değil.

### <a name="logging-authenticated-requests"></a>Kimlik doğrulaması günlüğe kaydetme istekleri
Kimliği doğrulanmış istekler türleri aşağıdaki hello kaydedilir:

* Başarılı istek sayısı.
* İstek zaman aşımı, azaltma, ağ, yetkilendirme ve başka hatalar da dahil olmak üzere, başarısız oldu.
* Başarılı ve başarısız istekleri dahil olmak üzere paylaşılan erişim imzası (SAS), kullanarak istek sayısı.
* İstekleri tooanalytics verileri.

Storage Analytics kendisini günlük oluşturma veya silme gibi tarafından yapılan istekleri günlüğe kaydedilmez. Oturum hello verilerin tam bir liste hello belgelenen [depolama Analytics günlüğe yazılan işlemler ve durum iletileri](https://msdn.microsoft.com/library/hh343260.aspx) ve [depolama Analytics günlük biçimi](https://msdn.microsoft.com/library/hh343259.aspx) Konular.

### <a name="logging-anonymous-requests"></a>Anonim istekler günlüğe kaydetme
Anonim istek türlerini aşağıdaki hello kaydedilir:

* Başarılı istek sayısı.
* Sunucu hataları.
* İstemci ve sunucu zaman aşımı hataları.
* Başarısız GET istekleri 304 hata koduyla (değişiklik).

Diğer tüm başarısız anonim istekler günlüğe kaydedilmez. Oturum hello verilerin tam bir liste hello belgelenen [depolama Analytics günlüğe yazılan işlemler ve durum iletileri](https://msdn.microsoft.com/library/hh343260.aspx) ve [depolama Analytics günlük biçimi](https://msdn.microsoft.com/library/hh343259.aspx) Konular.

### <a name="how-logs-are-stored"></a>Günlükleri nasıl depolanır
Tüm günlükler blok blobları Storage Analytics bir depolama hesabı için etkinleştirildiğinde, otomatik olarak oluşturulan $logs adlı bir kapsayıcıda depolanır. Merhaba $logs kapsayıcı bulunan hello blob ad alanında hello depolama hesabının, örneğin: `http://<accountname>.blob.core.windows.net/$logs`. Storage Analytics etkinleştirildikten sonra bu kapsayıcı içeriğini silinebilir silinemiyor.

> [!NOTE]
> İşlem listeleme bir kapsayıcı gerçekleştirildiğinde hello gibi Hello $logs kapsayıcı görüntülenmez [ListContainers](https://msdn.microsoft.com/library/azure/dd179352.aspx) yöntemi. Doğrudan erişim gerekir. Örneğin, hello kullanabilirsiniz [ListBlobs](https://msdn.microsoft.com/library/azure/dd135734.aspx) yöntemi tooaccess hello blobları hello `$logs` kapsayıcı.
> İstekleri günlüğe gibi depolama çözümlemeleri Ara sonuçların taşı olarak yükleyin. Düzenli aralıklarla, Storage Analytics bu blokları tamamlama ve bir blob olarak kullanılmasını.
> 
> 

Yinelenen kayıtları hello oluşturulan günlükleri için bulunabilir aynı saat. Merhaba denetleyerek bir kayıt yinelenen olup olmadığını belirleyebilirsiniz **RequestId** ve **işlemi** numarası.

### <a name="log-naming-conventions"></a>Günlük adlandırma kuralları
Her günlük biçimini izleyen hello yazılır.

    <service-name>/YYYY/MM/DD/hhmm/<counter>.log

Merhaba aşağıdaki tabloda her özniteliği hello günlük adında açıklanmaktadır.

| Öznitelik | Açıklama |
| --- | --- |
| < hizmet-adı > |Merhaba depolama hizmeti Hello adı. Örneğin: blob, tablo veya kuyruğu. |
| YYYY |Merhaba dört rakamlı yıl hello günlüğü. Örneğin: 2011. |
| MM |Merhaba iki basamaklı ay hello günlüğü. Örneğin: 07. |
| DD |Merhaba iki basamaklı ay hello günlüğü. Örneğin: 07. |
| ss |saat hello için başlangıç hello gösterir hello iki basamaklı saat, 24 saatlik UTC biçiminde kaydeder. Örneğin: 18. |
| mm |dakika hello günlükleri için başlangıç hello gösteren hello iki basamaklı bir sayı. Bu değer hello geçerli depolama çözümlemeleri sürümünde desteklenmiyor ve değeri her zaman 00 olacaktır. |
| <counter> |Altı basamaklı bir saat süre hello depolama hizmeti için oluşturulan günlük BLOB'ları hello sayısını gösteren sıfır tabanlı bir sayacı. Bu sayaç 000000 başlatır. Örneğin: 000001. |

Merhaba, hello önceki örneklerde birleştiren bir tam örnek günlük adını aşağıdadır.

    blob/2011/07/31/1800/000001.log

Merhaba, örnek kullanılan tooaccess hello önceki günlük olabilir URI aşağıdadır.

    https://<accountname>.blob.core.windows.net/$logs/blob/2011/07/31/1800/000001.log

Bir depolama istek günlüğe kaydedildiğinde hello elde edilen günlük adı hello işlemi tamamlandı istediğinizde toohello saat hatalarla ilintilidir. Örneğin, bir GetBlob istek 6: 30'da tamamlandı 7/31/2011'hello günlük önek aşağıdaki hello ile yazılacaktır:`blob/2011/07/31/1800/`

### <a name="log-metadata"></a>Log meta verileri
Tüm günlük BLOB'lar kullanılan tooidentify hangi günlük veri hello blob içeriyor olabilir meta verileriyle depolanır. Aşağıdaki tablonun hello her meta veri özniteliğinin açıklar.

| Öznitelik | Açıklama |
| --- | --- |
| LogType |Merhaba günlük tooread, yazma veya silme işlemleri ilgili bilgiler içeren olup olmadığını açıklar. Bu değer, bir tür veya üçünü virgülle ayrılmış bir birleşimini içerebilir. Örnek 1: yazma; Örnek 2: Okuma, yazma; Örnek 3: Okuma, yazma, silme. |
| StartTime |Merhaba YYYY hello biçiminde hello günlüğündeki bir girişi erken süresini-aa-: ssZ. Örneğin: 2011-07-31T18:21:46Z. |
| EndTime |Merhaba YYYY hello biçiminde hello günlüğündeki bir girişi son süresini-aa-: ssZ. Örneğin: 2011-07-31T18:22:09Z. |
| LogVersion |Merhaba günlük biçimi Hello sürümü. Şu anda 1.0 yalnızca desteklenen hello değerdir. |

Merhaba aşağıdaki listede hello önceki örnekler kullanarak tam örnek meta verilerini görüntüler.

* LogType yazma =
* StartTime 2011 =-07-31T18:21:46Z
* EndTime 2011 =-07-31T18:22:09Z
* LogVersion = 1.0

### <a name="accessing-logging-data"></a>Günlük verilerine erişme
Merhaba tüm verileri `$logs` kapsayıcı hello Blob hizmeti API'leri kullanılarak erişilebilir, hello .NET hello tarafından sağlanan API'lerini de dahil olmak üzere Azure kitaplığı yönetilen. Hello depolama hesabının yöneticisine okuma ve günlükleri, silme, ancak oluşturabilir veya bunları güncelleştirin. Merhaba günlüğün meta veri ve günlük adı için bir günlük sorgulanırken kullanılabilir. Verilen saatlik günlükleri tooappear için bozuk mümkündür, ancak hello meta veri, günlük girişlerinin hello timespan her zaman bir oturum açma belirtir.. Bu nedenle, belirli bir günlük için arama yaparken günlük adları ve meta verileri bir bileşimini kullanabilirsiniz.

## <a name="about-storage-analytics-metrics"></a>Storage Analytics ölçümleri hakkında
Storage Analytics istekleri tooa depolama hizmeti hakkında toplu işlem istatistiklerini ve kapasite verilerini dahil ölçümleri depolayabilirsiniz. İşlemler her iki hello API işlemi düzeyinde ve aynı zamanda hello depolama hizmeti düzeyinde bildirilir ve kapasite hello depolama hizmet düzeyinde bildirilir. Ölçüm verilerini kullanılan tooanalyze depolama hizmeti kullanım olması, hello depolama hizmeti ve tooimprove hello bir hizmeti kullanan uygulamaların performansını karşı yapılan istekleri ile sorunları tanılayın.

Storage Analytics toouse etkinleştirmeniz gerekir, tek tek her hizmet için toomonitor istediğiniz. Hello etkinleştirmek [Azure Portal](https://portal.azure.com). Ayrıntılar için bkz [hello Azure Portal'da depolama hesabı izleme](storage-monitor-storage-account.md). Storage Analytics hello REST API aracılığıyla programlı olarak veya hello istemci kitaplığı da etkinleştirebilirsiniz. Kullanım hello **hizmet özellikleri Al** her hizmet için işlemleri tooenable depolama çözümlemeleri.

### <a name="transaction-metrics"></a>İşlem ölçümlerini
Güçlü bir veri kümesi istenen API işlemi, giriş/çıkış, kullanılabilirlik, hatalar dahil olmak üzere her depolama hizmeti için saat veya dakika aralıklarla kaydedilir ve istek yüzdelerini kategorilere. Merhaba hello işlem ayrıntıları tam bir listesini görebilir [Storage Analytics Ölçüm tablosu şeması](https://msdn.microsoft.com/library/hh343264.aspx) konu.

İşlem verileri iki düzeyde – hello hizmet düzeyi ve hello API işlem düzeyinde kaydedilir. Merhaba hizmet düzeyinde hiçbir istek toohello hizmet yapılmışsa bile API işlemleri saatte tooa Tablo varlığı yazılan tüm özetlemeye istatistikleri istedi. Merhaba işlemi, bir saat içinde istediyseniz hello API işlemi, istatistikleri yalnızca yazılı tooan varlık düzeyindedir.

Örneğin, gerçekleştirdiğiniz bir **GetBlob** Blob Storage Analytics ölçümleri hizmetiniz işlemi oturum hello istek ve her ikisi de hello yanı sıra Blob hizmeti hello için toplanan hello verilerine dahil **GetBlob** işlemi. Ancak, yoksa **GetBlob** hello saatte istenen işlem, bir varlık toohello yazılmayacak `$MetricsTransactionsBlob` bu işlem için.

İşlem ölçümlerini, kullanıcı isteklerini ve depolama analizi tarafından kendisini yapılan istekleri için kaydedilir. Örneğin, depolama çözümlemeleri toowrite günlükleri ve tablo varlıkları isteklerinden kaydedilir. Bu istekler nasıl faturalandırılır hakkında daha fazla bilgi için bkz: [depolama çözümlemeleri ve faturalama](https://msdn.microsoft.com/library/hh360997.aspx).

### <a name="capacity-metrics"></a>Kapasite ölçümleri
> [!NOTE]
> Kapasite ölçümlerini şu anda yalnızca Merhaba Blob hizmeti olarak kullanılabilir. Merhaba tablo hizmeti ve sıra hizmeti için kapasite ölçümlerini Storage Analytics gelecekteki sürümlerinde kullanılabilir.
> 
> 

Kapasite verileri günlük bir depolama hesabının Blob hizmeti için kaydedilir ve iki tablo varlıkları yazılır. Bir varlık istatistikleri için kullanıcı verileri ve hello diğer sağlar hello hakkındaki istatistiklerdir `$logs` depolama analizi tarafından kullanılan blob kapsayıcısı. Merhaba `$MetricsCapacityBlob` tablo istatistikleri aşağıdaki hello içerir:

* **Kapasite**: hello bayt hello depolama hesabının Blob hizmeti tarafından kullanılan depolama alanı miktarı.
* **ContainerCount**: Merhaba hello depolama hesabının Blob hizmeti blob kapsayıcı sayısı.
* **ObjectCount**: Merhaba kaydedilmiş ve kaydedilmeyen bloğu ya da sayfa BLOB'ları hello depolama hesabının Blob hizmeti sayısı.

Merhaba kapasite ölçümleri hakkında daha fazla bilgi için bkz: [Storage Analytics Ölçüm tablosu şeması](https://msdn.microsoft.com/library/hh343264.aspx).

### <a name="how-metrics-are-stored"></a>Ölçümleri nasıl depolanır
Tüm ölçüm verilerini hello Depolama hizmetlerinin her biri için bu hizmet için ayrılmış üç tabloda depolanır: işlem bilgileri için bir tablo, dakikalık işlem bilgileri için bir tablo ve kapasite bilgileri için başka bir tablo. İstek ve yanıt verilerini işlem ve dakika işlem bilgilerini oluşur ve depolama alanı kullanım verilerini kapasite bilgilerini oluşur. Aşağıdaki tablonun hello açıklandığı gibi adlı tablolardaki saat ölçümleri, dakika ölçümleri ve bir depolama hesabının Blob hizmeti için kapasite erişilebilir.

| Ölçümleri düzeyi | Tablo adları | Desteklenen sürümler |
| --- | --- | --- |
| Saatlik ölçümleri, birincil konumu |$MetricsTransactionsBlob <br/>$MetricsTransactionsTable <br/> $MetricsTransactionsQueue |Sürümleri önceki too2013-08-15 yalnızca. Bu adları hala desteklenmektedir, ancak aşağıda listelenen toousing hello tabloları geçiş önerilir. |
| Saatlik ölçümleri, birincil konumu |$MetricsHourPrimaryTransactionsBlob <br/>$MetricsHourPrimaryTransactionsTable <br/>$MetricsHourPrimaryTransactionsQueue |2013-08-15 dahil olmak üzere tüm sürümleri. |
| Dakika ölçümleri, birincil konumu |$MetricsMinutePrimaryTransactionsBlob <br/>$MetricsMinutePrimaryTransactionsTable <br/>$MetricsMinutePrimaryTransactionsQueue |2013-08-15 dahil olmak üzere tüm sürümleri. |
| Saatlik ölçümleri, ikincil konum |$MetricsHourSecondaryTransactionsBlob <br/>$MetricsHourSecondaryTransactionsTable <br/>$MetricsHourSecondaryTransactionsQueue |2013-08-15 dahil olmak üzere tüm sürümleri. Okuma erişimli coğrafi olarak yedekli çoğaltma etkinleştirilmiş olması gerekir. |
| Dakika ölçümleri, ikincil konum |$MetricsMinuteSecondaryTransactionsBlob <br/>$MetricsMinuteSecondaryTransactionsTable <br/>$MetricsMinuteSecondaryTransactionsQueue |2013-08-15 dahil olmak üzere tüm sürümleri. Okuma erişimli coğrafi olarak yedekli çoğaltma etkinleştirilmiş olması gerekir. |
| Kapasite (yalnızca Blob hizmeti) |$MetricsCapacityBlob |2013-08-15 dahil olmak üzere tüm sürümleri. |

Storage Analytics bir depolama hesabı için etkinleştirildiğinde, bu tablolar otomatik olarak oluşturulur. Örneğin, hello depolama hesabı, başlangıç ad alanı erişilir:`https://<accountname>.table.core.windows.net/Tables("$MetricsTransactionsBlob")`

### <a name="accessing-metrics-data"></a>Ölçümleri verilerine erişme
Merhaba ölçümleri tablolarındaki tüm verileri hello tablo hizmeti API'leri kullanılarak erişilebilir, hello .NET hello tarafından sağlanan API'lerini de dahil olmak üzere Azure kitaplığı yönetilen. Hello depolama hesabının yöneticisine okuyun ve tablo varlıkları silmek, ancak oluşturabilir veya bunları güncelleştirin.

## <a name="billing-for-storage-analytics"></a>Depolama çözümlemeleri için fatura
Tüm ölçüm verilerini bir depolama hesabı hello Hizmetleri tarafından yazılır. Sonuç olarak, depolama analizi tarafından gerçekleştirilen her yazma işlemi faturalanabilir. Ayrıca, hello ölçüm verilerini tarafından kullanılan depolama alanı da Faturalanabilir miktarıdır.

Storage Analytics tarafından gerçekleştirilen eylemler şu hello Faturalanabilir şunlardır:

* Günlük için toocreate BLOB'lar ister. 
* Ölçümler için istekleri toocreate tablo varlıklar.

Bir veri bekletme ilkesi yapılandırdıysanız, depolama çözümlemeleri eski günlüğe kaydetme ve ölçüm verileri sildiğinde, silme işlemleri için sizden ücret istenmese. Ancak, bir istemciden silme işlemleri faturalanabilir. Bekletme ilkeleri hakkında daha fazla bilgi için bkz: [depolama Analytics veri Bekletme İlkesi ayarı](https://msdn.microsoft.com/library/azure/hh343263.aspx).

### <a name="understanding-billable-requests"></a>Faturalandırılabilir isteklerin anlama
Faturalanabilir ya da Faturalanamayan tooan hesabın depolama hizmeti yapılan her isteği değil. Storage Analytics hello isteği nasıl işlendiğini gösteren bir durum iletisi dahil tooa hizmetini yapılan her isteği günlüğe kaydeder. Benzer şekilde, Storage Analytics ölçümleri hello yüzdeleri ve belirli durum iletilerinin sayısını da dahil olmak üzere bu hizmetinin hem hizmet hem de hello API işlemleri için depolar. Birlikte, bu özellikler, uygulamanızda geliştirmeler yapmak ve istekleri tooyour Hizmetleri ile ilgili sorunları tanılamak Faturalanabilir isteklerinizi çözümlemenize yardımcı olabilir. Faturalama hakkında daha fazla bilgi için bkz: [anlama Azure depolama faturalama - bant genişliği, işlemleri ve kapasite](http://blogs.msdn.com/b/windowsazurestorage/archive/2010/07/09/understanding-windows-azure-storage-billing-bandwidth-transactions-and-capacity.aspx).

Storage Analytics veri bakarken hello hello tabloları kullanabilir [depolama Analytics günlüğe yazılan işlemler ve durum iletileri](https://msdn.microsoft.com/library/azure/hh343260.aspx) hangi isteklerin olduğu Faturalanabilir konu toodetermine. Ardından, belirli bir istek için sizden ücret günlükleri ve ölçümleri veri toohello durum iletileri toosee karşılaştırabilirsiniz. Önceki konu tooinvestigate kullanılabilirlik hello bir depolama birimi hizmeti veya bireysel API işlemi için hello tabloları kullanabilir.

## <a name="next-steps"></a>Sonraki adımlar
### <a name="setting-up-storage-analytics"></a>Storage Analytics ayarlama
* [İzleyici hello Azure Portal'da depolama hesabı](storage-monitor-storage-account.md)
* [Etkinleştirme ve depolama çözümlemeleri yapılandırma](https://msdn.microsoft.com/library/hh360996.aspx)

### <a name="storage-analytics-logging"></a>Storage Analytics günlüğe kaydetme
* [Storage Analytics günlüğü hakkında](https://msdn.microsoft.com/library/hh343262.aspx)
* [Storage Analytics günlük biçimi](https://msdn.microsoft.com/library/hh343259.aspx)
* [Storage Analytics işlemler ve durum iletilerini günlüğe](https://msdn.microsoft.com/library/hh343260.aspx)

### <a name="storage-analytics-metrics"></a>Storage Analytics ölçümleri
* [Storage Analytics ölçümleri hakkında](https://msdn.microsoft.com/library/hh343258.aspx)
* [Storage Analytics Ölçüm tablosu şeması](https://msdn.microsoft.com/library/hh343264.aspx)
* [Storage Analytics işlemler ve durum iletilerini günlüğe](https://msdn.microsoft.com/library/hh343260.aspx)  

