---
title: "aaaAzure İzleyici ölçümleri - kaynak türü başına desteklenen ölçümleri | Microsoft Docs"
description: "Azure İzleyicisi ile her bir kaynak türü için kullanılabilir ölçümleri listesi."
author: johnkemnetz
manager: orenr
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: 63d4ac65-1688-40d1-85c8-7cd408285b0f
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 7/05/2017
ms.author: johnkem
ms.openlocfilehash: 66834238a1a4fcd7db1464cc023c18ee2563517a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="supported-metrics-with-azure-monitor"></a>Azure İzleyicisi ile desteklenen ölçümleri
Azure İzleyicisi'nin sağladığı çeşitli yolları toointeract hello Portalı'nda grafik hello REST API erişme veya bunları sorgulama dahil olmak üzere Ölçümleriyle PowerShell veya CLI kullanarak. Aşağıda tüm ölçümleri tam bir listesi ile Azure monitörün ölçüm ardışık düzen şu anda kullanılabilir.

> [!NOTE]
> Merhaba portalı veya eski API'lerini kullanarak diğer ölçümleri bulunabilir. Bu liste, yalnızca genel Önizleme ölçümleri hello genel Önizleme birleştirilmiş hello Azure İzleyici ölçüm ardışık kullanarak kullanılabilir içerir.
>
>

## <a name="microsoftanalysisservicesservers"></a>Microsoft.AnalysisServices/servers

|Ölçüm|Ölçüm görünen adı|Birim|Toplama türü|Açıklama|
|---|---|---|---|---|
|qpu_metric|QPU|Sayı|Ortalama|QPU. S1, S2 için 0-200 ve 0-400 S4 için için 0-100 aralığında|
|memory_metric|Bellek|Bayt|Ortalama|Bellek. 0-25 GB S1, S2 için 0-50 GB ve 0-100 aralığında S4 için GB|
|TotalConnectionRequests|Toplam bağlantı istekleri|Sayı|Ortalama|Toplam bağlantı istekleri. Varış bunlar.|
|SuccessfullConnectionsPerSec|Başarılı bağlantıları sayısı / sn|CountPerSecond|Ortalama|Başarılı bağlantının tamamlamalar oranı.|
|TotalConnectionFailures|Toplam bağlantı hataları|Sayı|Ortalama|Toplam bağlantı denemesi başarısız oldu.|
|CurrentUserSessions|Geçerli kullanıcı oturumları|Sayı|Ortalama|Oluşturulan kullanıcı oturumları geçerli sayısı.|
|QueryPoolBusyThreads|Sorgu havuzu meşgul iş parçacıkları|Sayı|Ortalama|Meşgul hello sorgu iş parçacığı havuzu iş parçacıkları sayısı.|
|CommandPoolJobQueueLength|Komut havuzu iş sırası uzunluğu|Sayı|Ortalama|Merhaba komutu iş parçacığı havuzunun hello sırasındaki işlerin sayısı.|
|ProcessingPoolJobQueueLength|İşlem havuzu iş sırası uzunluğu|Sayı|Ortalama|İş parçacığı havuzu işleme hello hello sırasındaki olmayan-g/Ç işlerin sayısı.|
|CurrentConnections|Bağlantı: Geçerli bağlantılar|Sayı|Ortalama|İstemci bağlantı kuran geçerli sayısı.|
|CleanerCurrentPrice|Bellek: Temizleyici geçerli fiyatı|Sayı|Ortalama|Geçerli fiyat bellek, bayt / $/ saat, normalleştirilmiş too1000.|
|CleanerMemoryShrinkable|: Temizleyici bellek daraltılabilir|Bayt|Ortalama|Bellek miktarını bayt cinsinden hello arka plan temizleyici tarafından konu toopurging.|
|CleanerMemoryNonshrinkable|Bellek: Temizleyici bellek nonshrinkable|Bayt|Ortalama|Bellek miktarını bayt cinsinden konu toopurging hello arka plan temizleyici tarafından değil.|
|MemoryUsage|Bellek: Bellek kullanımı|Bayt|Ortalama|Temizleyici bellek fiyatı hesaplamak için kullanılan gibi hello sunucu işleminin bellek kullanımını. Bellek eşlemeli veri olan eşlenen veya hello xVelocity altyapısı bellek sınırı aşan hello xVelocity bellek içi analytics altyapısı (VertiPaq) tarafından ayrılan bellek yoksayılıyor toocounter Process\PrivateBytes artı hello boyutu eşit.|
|MemoryLimitHard|Bellek: Sabit bellek sınırı|Bayt|Ortalama|Yapılandırma dosyasından sabit bellek sınırı.|
|MemoryLimitHigh|Bellek: Bellek sınırı yüksek|Bayt|Ortalama|Yapılandırma dosyasından yüksek bellek sınırı.|
|MemoryLimitLow|Bellek: Bellek sınırı düşük|Bayt|Ortalama|Yapılandırma dosyasından düşük bellek sınırı.|
|MemoryLimitVertiPaq|Bellek: Bellek sınırı VertiPaq|Bayt|Ortalama|Yapılandırma dosyasından bellek içi sınırı.|
|Kota|Bellek: Kota|Bayt|Ortalama|Bayt cinsinden geçerli bellek kotasını. Bellek kotasını bellek grant veya bellek ayırma de denir.|
|QuotaBlocked|Bellek: Engellenen kota|Sayı|Ortalama|Geçerli diğer bellek kotalarını serbest kadar engellenen kota istek sayısı.|
|VertiPaqNonpaged|Bellek: VertiPaq belleği olmayan havuz|Bayt|Ortalama|Bayt bellek kullanmak için hello çalışma kümesindeki hello bellek içi altyapısı tarafından kilitlenmiş.|
|VertiPaqPaged|Bellek: Disk belleği VertiPaq|Bayt|Ortalama|Bellek içi veriler için kullanılan disk belleği bayt.|
|RowsReadPerSec|İşlem: Satır sayısı / sn okuyun.|CountPerSecond|Ortalama|Satır oranını tüm ilişkisel veritabanlarından okuyun.|
|RowsConvertedPerSec|İşlem: Satır sayısı / sn dönüştürülür.|CountPerSecond|Ortalama|İşleme sırasında dönüştürülmüş satır oranı.|
|RowsWrittenPerSec|İşlem: saniye yazılan satırları|CountPerSecond|Ortalama|İşleme sırasında yazılmış satırları oranı.|
|CommandPoolBusyThreads|İş parçacıkları: Komut havuzu meşgul iş parçacıkları|Sayı|Ortalama|Meşgul hello komutu iş parçacığı havuzu iş parçacıkları sayısı.|
|CommandPoolIdleThreads|İş parçacıkları: boş iş parçacığı havuzu komutu|Sayı|Ortalama|Merhaba komutu iş parçacığı havuzundaki boş iş parçacığı sayısı.|
|LongParsingBusyThreads|İş parçacıkları: meşgul iş parçacığı ayrıştırma uzun|Sayı|Ortalama|İş parçacığı havuzu uzun ayrıştırma hello meşgul iş parçacığı sayısı.|
|LongParsingIdleThreads|İş parçacıkları: boş iş parçacığı ayrıştırma uzun|Sayı|Ortalama|İş parçacığı havuzu uzun ayrıştırma hello boş iş parçacığı sayısı.|
|LongParsingJobQueueLength|İş parçacıkları: Uzun iş kuyruğu uzunluğu ayrıştırma|Sayı|Ortalama|İş parçacığı havuzu uzun ayrıştırma hello hello sırasındaki işlerin sayısı.|
|ProcessingPoolBusyIOJobThreads|İş parçacıkları: havuz meşgul g/ç iş iş parçacığı işleme|Sayı|Ortalama|Çalışan iş parçacığı havuzu işleme hello g/ç iş iş parçacığı sayısı.|
|ProcessingPoolBusyNonIOThreads|İş parçacıkları: yoğun olmayan-g/Ç iş parçacığı havuzu işleme|Sayı|Ortalama|Çalışan iş parçacığı havuzu işleme hello olmayan-g/Ç iş iş parçacığı sayısı.|
|ProcessingPoolIOJobQueueLength|İş parçacıkları: işleme havuzu g/ç iş sırası uzunluğu|Sayı|Ortalama|İş parçacığı havuzu işleme hello hello sırasındaki g/ç işlerin sayısı.|
|ProcessingPoolIdleIOJobThreads|İş parçacıkları: havuz boşta g/ç iş iş parçacığı işleme|Sayı|Ortalama|İş parçacığı havuzu işleme hello g/ç işleri için boş iş parçacığı sayısı.|
|ProcessingPoolIdleNonIOThreads|İş parçacıkları: boş olmayan-g/Ç iş parçacığı havuzu işleme|Sayı|Ortalama|İş parçacığı havuzu işleme hello içindeki boş iş parçacığı sayısı toonon-g/Ç işleri ayrılmış.|
|QueryPoolIdleThreads|İş parçacıkları: Sorgu havuzu boşta iş parçacıkları|Sayı|Ortalama|İş parçacığı havuzu işleme hello g/ç işleri için boş iş parçacığı sayısı.|
|QueryPoolJobQueueLength|İş parçacıkları: Sorgu havuzu iş kuyruğu lengt|Sayı|Ortalama|Merhaba sorgu iş parçacığı havuzunun hello sırasındaki işlerin sayısı.|
|ShortParsingBusyThreads|İş parçacıkları: meşgul iş parçacığı ayrıştırma kısa|Sayı|Ortalama|İş parçacığı havuzu ayrıştırma kısa hello meşgul iş parçacığı sayısı.|
|ShortParsingIdleThreads|İş parçacıkları: boş iş parçacığı ayrıştırma kısa|Sayı|Ortalama|İş parçacığı havuzu ayrıştırma kısa hello boş iş parçacığı sayısı.|
|ShortParsingJobQueueLength|İş parçacıkları: İş kuyruğu uzunluğu ayrıştırma kısa|Sayı|Ortalama|İş parçacığı havuzu ayrıştırma kısa hello hello sırasındaki işlerin sayısı.|
|memory_thrashing_metric|Bellek yoğun disk belleği|Yüzde|Ortalama|Ortalama bellek yoğun disk belleği'ü tıklatın.|

## <a name="microsoftapimanagementservice"></a>Microsoft.ApiManagement/service

|Ölçüm|Ölçüm görünen adı|Birim|Toplama türü|Açıklama|
|---|---|---|---|---|
|TotalRequests|Toplam ağ geçidi istekleri|Sayı|Toplam|Ağ geçidi istek sayısı|
|SuccessfulRequests|Başarılı ağ geçidi istekleri|Sayı|Toplam|Başarılı ağ geçidi istek sayısı|
|UnauthorizedRequests|Yetkisiz ağ geçidi istekleri|Sayı|Toplam|Yetkisiz ağ geçidi istek sayısı|
|FailedRequests|Başarısız ağ geçidi istekleri|Sayı|Toplam|Ağ geçidi istek sayısı|
|OtherRequests|Diğer ağ geçidi istekleri|Sayı|Toplam|Diğer ağ geçidi istek sayısı|

## <a name="microsoftbatchbatchaccounts"></a>Microsoft.Batch/batchAccounts

|Ölçüm|Ölçüm görünen adı|Birim|Toplama türü|Açıklama|
|---|---|---|---|---|
|CoreCount|Ayrılmış çekirdek sayısı|Sayı|Toplam|Ayrılmış çekirdek hello toplu işlem hesabı ile toplam sayısı|
|TotalNodeCount|Ayrılmış düğüm sayısı|Sayı|Toplam|Merhaba toplu işlem hesabı ayrılmış düğümlerin toplam sayısı|
|LowPriorityCoreCount|LowPriority çekirdek sayısı|Sayı|Toplam|Düşük öncelikli çekirdek hello toplu işlem hesabı ile toplam sayısı|
|TotalLowPriorityNodeCount|Düşük öncelikli düğüm sayısı|Sayı|Toplam|Düşük öncelikli düğüm hello batch hesabındaki toplam sayısı|
|CreatingNodeCount|Düğüm sayısı oluşturma|Sayı|Toplam|Oluşturulan düğüm sayısı|
|StartingNodeCount|Başlangıç düğüm sayısı|Sayı|Toplam|Başlangıç düğüm sayısı|
|WaitingForStartTaskNodeCount|Başlangıç görevi düğüm sayısı için bekleniyor|Sayı|Toplam|Başlangıç görevi Başlat toocomplete için bekleyen düğüm sayısı|
|StartTaskFailedNodeCount|Düğüm sayısı başlangıç görevi başarısız oldu|Sayı|Toplam|Başlangıç görevi başlat başarısız olduğu düğüm sayısı|
|IdleNodeCount|Boşta düğüm sayısı|Sayı|Toplam|Boşta düğüm sayısı|
|OfflineNodeCount|Çevrimdışı düğüm sayısı|Sayı|Toplam|Çevrimdışı düğüm sayısı|
|RebootingNodeCount|Düğüm sayısı yeniden başlatılıyor|Sayı|Toplam|Düğüm yeniden başlatma sayısı|
|ReimagingNodeCount|Düğüm sayısı yeniden görüntüleme|Sayı|Toplam|Yeniden görüntüsünü oluşturuyor düğüm sayısı|
|RunningNodeCount|Çalışan düğüm sayısı|Sayı|Toplam|Düğümler çalışan sayısı|
|LeavingPoolNodeCount|Bırakma havuzu düğüm sayısı|Sayı|Toplam|Merhaba havuzu bırakarak düğüm sayısı|
|UnusableNodeCount|Kullanılamaz düğüm sayısı|Sayı|Toplam|Kullanılamaz düğüm sayısı|
|PreemptedNodeCount|Etkisiz düğüm sayısı|Sayı|Toplam|Etkisiz düğüm sayısı|
|TaskStartEvent|Görev Başlangıç olayları|Sayı|Toplam|Başlattığınız görevlerin toplam sayısı|
|TaskCompleteEvent|Görev Tamamlandı olayları|Sayı|Toplam|Tamamlanan görevler toplam sayısı|
|TaskFailEvent|Görev başarısız olayları|Sayı|Toplam|Başarısız bir durumda tamamlanan görevler toplam sayısı|
|PoolCreateEvent|Havuz oluşturma olayları|Sayı|Toplam|Oluşturulmuş havuzu toplam sayısı|
|PoolResizeStartEvent|Havuzu yeniden boyutlandırma başlangıç olayları|Sayı|Toplam|Başlattığınız havuzu yeniden boyutlandırır toplam sayısı|
|PoolResizeCompleteEvent|Havuzu yeniden boyutlandırma tam olayları|Sayı|Toplam|Tamamlanan havuzu yeniden boyutlandırır toplam sayısı|
|PoolDeleteStartEvent|Havuz başlangıç olayları Sil|Sayı|Toplam|Başlattığınız havuzu siler toplam sayısı|
|PoolDeleteCompleteEvent|Havuz tüm olayları Sil|Sayı|Toplam|Tamamlanan havuzu siler toplam sayısı|

## <a name="microsoftcacheredis"></a>Microsoft.Cache/redis

|Ölçüm|Ölçüm görünen adı|Birim|Toplama türü|Açıklama|
|---|---|---|---|---|
|connectedclients|Bağlanan istemciler|Sayı|Maksimum||
|totalcommandsprocessed|Toplam işlemler|Sayı|Toplam||
|cachehits|İsabetli Önbellek okuma sayısı|Sayı|Toplam||
|cachemisses|İsabetsiz önbellek okuma sayısı|Sayı|Toplam||
|getcommands|Alır|Sayı|Toplam||
|setcommands|Ayarlar|Sayı|Toplam||
|evictedkeys|Çıkarılan anahtarları|Sayı|Toplam||
|totalkeys|Toplam anahtarları|Sayı|Maksimum||
|expiredkeys|Süresi dolan anahtarları|Sayı|Toplam||
|usedmemory|Kullanılan bellek|Bayt|Maksimum||
|usedmemoryRss|Kullanılan bellek RSS|Bayt|Maksimum||
|serverLoad|Sunucu iş yükü|Yüzde|Maksimum||
|cacheWrite|Önbellek yazma|BytesPerSecond|Maksimum||
|cacheRead|Önbellek Okuma|BytesPerSecond|Maksimum||
|percentProcessorTime|CPU|Yüzde|Maksimum||
|connectedclients0|Bağlanan istemciler (parça 0)|Sayı|Maksimum||
|totalcommandsprocessed0|Toplam işlemler (parça 0)|Sayı|Toplam||
|cachehits0|İsabetli Önbellek Okuma (parça 0)|Sayı|Toplam||
|cachemisses0|Önbellek isabetsizliği (parça 0)|Sayı|Toplam||
|getcommands0|(Parça 0) alır|Sayı|Toplam||
|setcommands0|Ayarlar (parça 0)|Sayı|Toplam||
|evictedkeys0|Çıkarılan anahtarları (parça 0)|Sayı|Toplam||
|totalkeys0|Toplam anahtarları (parça 0)|Sayı|Maksimum||
|expiredkeys0|Süresi dolan anahtarları (parça 0)|Sayı|Toplam||
|usedmemory0|Kullanılan bellek (parça 0)|Bayt|Maksimum||
|usedmemoryRss0|Kullanılan bellek RSS (parça 0)|Bayt|Maksimum||
|serverLoad0|Sunucu iş yükü (parça 0)|Yüzde|Maksimum||
|cacheWrite0|Önbellek yazma (parça 0)|BytesPerSecond|Maksimum||
|cacheRead0|Önbellek Okuma (parça 0)|BytesPerSecond|Maksimum||
|percentProcessorTime0|CPU (parça 0)|Yüzde|Maksimum||
|connectedclients1|Bağlanan istemciler (parça 1)|Sayı|Maksimum||
|totalcommandsprocessed1|Toplam işlemler (parça 1)|Sayı|Toplam||
|cachehits1|İsabetli Önbellek Okuma (parça 1)|Sayı|Toplam||
|cachemisses1|Önbellek isabetsizliği (parça 1)|Sayı|Toplam||
|getcommands1|(Parça 1) alır|Sayı|Toplam||
|setcommands1|Ayarlar (parça 1)|Sayı|Toplam||
|evictedkeys1|Çıkarılan anahtarları (parça 1)|Sayı|Toplam||
|totalkeys1|Toplam anahtarları (parça 1)|Sayı|Maksimum||
|expiredkeys1|Süresi dolan anahtarları (parça 1)|Sayı|Toplam||
|usedmemory1|Kullanılan bellek (parça 1)|Bayt|Maksimum||
|usedmemoryRss1|Kullanılan bellek RSS (parça 1)|Bayt|Maksimum||
|serverLoad1|Sunucu iş yükü (parça 1)|Yüzde|Maksimum||
|cacheWrite1|Önbellek yazma (parça 1)|BytesPerSecond|Maksimum||
|cacheRead1|Önbellek Okuma (parça 1)|BytesPerSecond|Maksimum||
|percentProcessorTime1|CPU (parça 1)|Yüzde|Maksimum||
|connectedclients2|Bağlanan istemciler (parça 2)|Sayı|Maksimum||
|totalcommandsprocessed2|Toplam işlemler (parça 2)|Sayı|Toplam||
|cachehits2|İsabetli Önbellek Okuma (parça 2)|Sayı|Toplam||
|cachemisses2|Önbellek isabetsizliği (parça 2)|Sayı|Toplam||
|getcommands2|(Parça 2) alır|Sayı|Toplam||
|setcommands2|Ayarlar (parça 2)|Sayı|Toplam||
|evictedkeys2|Çıkarılan anahtarları (parça 2)|Sayı|Toplam||
|totalkeys2|Toplam anahtarları (parça 2)|Sayı|Maksimum||
|expiredkeys2|Süresi dolan anahtarları (parça 2)|Sayı|Toplam||
|usedmemory2|Kullanılan bellek (parça 2)|Bayt|Maksimum||
|usedmemoryRss2|Kullanılan bellek RSS (parça 2)|Bayt|Maksimum||
|serverLoad2|Sunucu iş yükü (parça 2)|Yüzde|Maksimum||
|cacheWrite2|Önbellek yazma (parça 2)|BytesPerSecond|Maksimum||
|cacheRead2|Önbellek Okuma (parça 2)|BytesPerSecond|Maksimum||
|percentProcessorTime2|CPU (parça 2)|Yüzde|Maksimum||
|connectedclients3|Bağlanan istemciler (parça 3)|Sayı|Maksimum||
|totalcommandsprocessed3|Toplam işlemler (parça 3)|Sayı|Toplam||
|cachehits3|İsabetli Önbellek Okuma (parça 3)|Sayı|Toplam||
|cachemisses3|Önbellek isabetsizliği (parça 3)|Sayı|Toplam||
|getcommands3|(3 parça) alır|Sayı|Toplam||
|setcommands3|Ayarlar (parça 3)|Sayı|Toplam||
|evictedkeys3|Çıkarılan anahtarları (parça 3)|Sayı|Toplam||
|totalkeys3|Toplam anahtarları (parça 3)|Sayı|Maksimum||
|expiredkeys3|Süresi dolan anahtarları (parça 3)|Sayı|Toplam||
|usedmemory3|Kullanılan bellek (parça 3)|Bayt|Maksimum||
|usedmemoryRss3|Kullanılan bellek RSS (parça 3)|Bayt|Maksimum||
|serverLoad3|Sunucu iş yükü (parça 3)|Yüzde|Maksimum||
|cacheWrite3|Önbellek yazma (parça 3)|BytesPerSecond|Maksimum||
|cacheRead3|Önbellek Okuma (parça 3)|BytesPerSecond|Maksimum||
|percentProcessorTime3|CPU (parça 3)|Yüzde|Maksimum||
|connectedclients4|Bağlanan istemciler (parça 4)|Sayı|Maksimum||
|totalcommandsprocessed4|Toplam işlemler (parça 4)|Sayı|Toplam||
|cachehits4|İsabetli Önbellek Okuma (parça 4)|Sayı|Toplam||
|cachemisses4|Önbellek isabetsizliği (parça 4)|Sayı|Toplam||
|getcommands4|(4 parça) alır|Sayı|Toplam||
|setcommands4|Ayarlar (parça 4)|Sayı|Toplam||
|evictedkeys4|Çıkarılan anahtarları (parça 4)|Sayı|Toplam||
|totalkeys4|Toplam anahtarları (parça 4)|Sayı|Maksimum||
|expiredkeys4|Süresi dolan anahtarları (parça 4)|Sayı|Toplam||
|usedmemory4|Kullanılan bellek (parça 4)|Bayt|Maksimum||
|usedmemoryRss4|Kullanılan bellek RSS (parça 4)|Bayt|Maksimum||
|serverLoad4|Sunucu iş yükü (parça 4)|Yüzde|Maksimum||
|cacheWrite4|Önbellek yazma (parça 4)|BytesPerSecond|Maksimum||
|cacheRead4|Önbellek Okuma (parça 4)|BytesPerSecond|Maksimum||
|percentProcessorTime4|CPU (parça 4)|Yüzde|Maksimum||
|connectedclients5|Bağlanan istemciler (parça 5)|Sayı|Maksimum||
|totalcommandsprocessed5|Toplam işlemler (parça 5)|Sayı|Toplam||
|cachehits5|İsabetli Önbellek Okuma (parça 5)|Sayı|Toplam||
|cachemisses5|Önbellek isabetsizliği (parça 5)|Sayı|Toplam||
|getcommands5|(5 parça) alır|Sayı|Toplam||
|setcommands5|Ayarlar (parça 5)|Sayı|Toplam||
|evictedkeys5|Çıkarılan anahtarları (parça 5)|Sayı|Toplam||
|totalkeys5|Toplam anahtarları (parça 5)|Sayı|Maksimum||
|expiredkeys5|Süresi dolan anahtarları (parça 5)|Sayı|Toplam||
|usedmemory5|Kullanılan bellek (parça 5)|Bayt|Maksimum||
|usedmemoryRss5|Kullanılan bellek RSS (parça 5)|Bayt|Maksimum||
|serverLoad5|Sunucu iş yükü (parça 5)|Yüzde|Maksimum||
|cacheWrite5|Önbellek yazma (parça 5)|BytesPerSecond|Maksimum||
|cacheRead5|Önbellek Okuma (parça 5)|BytesPerSecond|Maksimum||
|percentProcessorTime5|CPU (parça 5)|Yüzde|Maksimum||
|connectedclients6|Bağlanan istemciler (parça 6)|Sayı|Maksimum||
|totalcommandsprocessed6|Toplam işlemler (parça 6)|Sayı|Toplam||
|cachehits6|İsabetli Önbellek Okuma (parça 6)|Sayı|Toplam||
|cachemisses6|Önbellek isabetsizliği (parça 6)|Sayı|Toplam||
|getcommands6|(Parça 6) alır|Sayı|Toplam||
|setcommands6|Ayarlar (parça 6)|Sayı|Toplam||
|evictedkeys6|Çıkarılan anahtarları (parça 6)|Sayı|Toplam||
|totalkeys6|Toplam anahtarları (parça 6)|Sayı|Maksimum||
|expiredkeys6|Süresi dolan anahtarları (parça 6)|Sayı|Toplam||
|usedmemory6|Kullanılan bellek (parça 6)|Bayt|Maksimum||
|usedmemoryRss6|Kullanılan bellek RSS (parça 6)|Bayt|Maksimum||
|serverLoad6|Sunucu iş yükü (parça 6)|Yüzde|Maksimum||
|cacheWrite6|Önbellek yazma (parça 6)|BytesPerSecond|Maksimum||
|cacheRead6|Önbellek Okuma (parça 6)|BytesPerSecond|Maksimum||
|percentProcessorTime6|CPU (parça 6)|Yüzde|Maksimum||
|connectedclients7|Bağlanan istemciler (parça 7)|Sayı|Maksimum||
|totalcommandsprocessed7|Toplam işlemler (parça 7)|Sayı|Toplam||
|cachehits7|İsabetli Önbellek Okuma (parça 7)|Sayı|Toplam||
|cachemisses7|Önbellek isabetsizliği (parça 7)|Sayı|Toplam||
|getcommands7|(Parça 7) alır|Sayı|Toplam||
|setcommands7|Ayarlar (parça 7)|Sayı|Toplam||
|evictedkeys7|Çıkarılan anahtarları (parça 7)|Sayı|Toplam||
|totalkeys7|Toplam anahtarları (parça 7)|Sayı|Maksimum||
|expiredkeys7|Süresi dolan anahtarları (parça 7)|Sayı|Toplam||
|usedmemory7|Kullanılan bellek (parça 7)|Bayt|Maksimum||
|usedmemoryRss7|Kullanılan bellek RSS (parça 7)|Bayt|Maksimum||
|serverLoad7|Sunucu iş yükü (parça 7)|Yüzde|Maksimum||
|cacheWrite7|Önbellek yazma (parça 7)|BytesPerSecond|Maksimum||
|cacheRead7|Önbellek Okuma (parça 7)|BytesPerSecond|Maksimum||
|percentProcessorTime7|CPU (parça 7)|Yüzde|Maksimum||
|connectedclients8|Bağlanan istemciler (parça 8)|Sayı|Maksimum||
|totalcommandsprocessed8|Toplam işlemler (parça 8)|Sayı|Toplam||
|cachehits8|İsabetli Önbellek Okuma (parça 8)|Sayı|Toplam||
|cachemisses8|Önbellek isabetsizliği (parça 8)|Sayı|Toplam||
|getcommands8|(Parça 8) alır|Sayı|Toplam||
|setcommands8|Ayarlar (parça 8)|Sayı|Toplam||
|evictedkeys8|Çıkarılan anahtarları (parça 8)|Sayı|Toplam||
|totalkeys8|Toplam anahtarları (parça 8)|Sayı|Maksimum||
|expiredkeys8|Süresi dolan anahtarları (parça 8)|Sayı|Toplam||
|usedmemory8|Kullanılan bellek (parça 8)|Bayt|Maksimum||
|usedmemoryRss8|Kullanılan bellek RSS (parça 8)|Bayt|Maksimum||
|serverLoad8|Sunucu iş yükü (parça 8)|Yüzde|Maksimum||
|cacheWrite8|Önbellek yazma (parça 8)|BytesPerSecond|Maksimum||
|cacheRead8|Önbellek Okuma (parça 8)|BytesPerSecond|Maksimum||
|percentProcessorTime8|CPU (parça 8)|Yüzde|Maksimum||
|connectedclients9|Bağlanan istemciler (parça 9)|Sayı|Maksimum||
|totalcommandsprocessed9|Toplam işlemler (parça 9)|Sayı|Toplam||
|cachehits9|İsabetli Önbellek Okuma (parça 9)|Sayı|Toplam||
|cachemisses9|Önbellek isabetsizliği (parça 9)|Sayı|Toplam||
|getcommands9|Alır (parça 9)|Sayı|Toplam||
|setcommands9|Ayarlar (parça 9)|Sayı|Toplam||
|evictedkeys9|Çıkarılan anahtarları (parça 9)|Sayı|Toplam||
|totalkeys9|Toplam anahtarları (parça 9)|Sayı|Maksimum||
|expiredkeys9|Süresi dolan anahtarları (parça 9)|Sayı|Toplam||
|usedmemory9|Kullanılan bellek (parça 9)|Bayt|Maksimum||
|usedmemoryRss9|Kullanılan bellek RSS (parça 9)|Bayt|Maksimum||
|serverLoad9|Sunucu iş yükü (parça 9)|Yüzde|Maksimum||
|cacheWrite9|Önbellek yazma (parça 9)|BytesPerSecond|Maksimum||
|cacheRead9|Önbellek Okuma (parça 9)|BytesPerSecond|Maksimum||
|percentProcessorTime9|CPU (parça 9)|Yüzde|Maksimum||

## <a name="microsoftcognitiveservicesaccounts"></a>Microsoft.CognitiveServices/accounts

|Ölçüm|Ölçüm görünen adı|Birim|Toplama türü|Açıklama|
|---|---|---|---|---|
|TotalCalls|Toplam çağrı sayısı|Sayı|Toplam|Toplam çağrı sayısı.|
|SuccessfulCalls|Başarılı çağrıları|Sayı|Toplam|Başarılı çağrı sayısı.|
|TotalErrors|Toplam hata|Sayı|Toplam|Toplam hata yanıtı (HTTP yanıt kodu 4xx veya 5xx) ile çağrı sayısı.|
|BlockedCalls|Engellenen Aramalar|Sayı|Toplam|Bu aşıldı oranı veya kota sınırı çağrı sayısı.|
|ServerErrors|Sunucu hataları|Sayı|Toplam|Hizmet iç hatası (HTTP yanıt kodu 5xx) ile çağrı sayısı.|
|ClientErrors|İstemci hataları|Sayı|Toplam|İstemci tarafı hatası (HTTP yanıt kodu 4xx) ile çağrı sayısı.|
|Elinden|Verileri|Bayt|Toplam|Gelen veri bayt cinsinden boyutu.|
|DataOut|Giden veriler|Bayt|Toplam|Giden veri bayt cinsinden boyutu.|
|Gecikme süresi|Gecikme süresi|Milisaniye|Ortalama|Milisaniye cinsinden gecikme süresi.|

## <a name="microsoftcomputevirtualmachines"></a>Microsoft.Compute/virtualMachines

|Ölçüm|Ölçüm görünen adı|Birim|Toplama türü|Açıklama|
|---|---|---|---|---|
|CPU yüzdesi|CPU yüzdesi|Yüzde|Ortalama|şu anda hello sanal makineleri tarafından kullanılmakta olan ayrılmış işlem birimleri Hello yüzdesi|
|Ağ içine|Ağ içine|Bayt|Toplam|Merhaba tüm ağ arabirimlerindeki hello sanal makineleri (gelen trafiği) tarafından alınan bayt sayısı|
|Ağ dışına|Ağ dışına|Bayt|Toplam|Merhaba out tüm ağ arabirimlerindeki hello sanal makineleri (giden trafiği) tarafından bayt sayısı|
|Disk okuma bayt|Disk okuma bayt|Bayt|Toplam|İzleme süresi sırasında diskten okunan toplam bayt sayısı|
|Disk yazma bayt|Disk yazma bayt|Bayt|Toplam|İzleme süresi sırasında toodisk yazılan toplam bayt|
|Disk okuma işlemleri/sn|Disk okuma işlemleri/sn|CountPerSecond|Ortalama|Disk okuma IOPS|
|Disk yazma işlemi/sn|Disk yazma işlemi/sn|CountPerSecond|Ortalama|Disk yazma IOPS|

## <a name="microsoftcomputevirtualmachinescalesets"></a>Microsoft.Compute/virtualMachineScaleSets

|Ölçüm|Ölçüm görünen adı|Birim|Toplama türü|Açıklama|
|---|---|---|---|---|
|CPU yüzdesi|CPU yüzdesi|Yüzde|Ortalama|şu anda hello sanal makineleri tarafından kullanılmakta olan ayrılmış işlem birimleri Hello yüzdesi|
|Ağ içine|Ağ içine|Bayt|Toplam|Merhaba tüm ağ arabirimlerindeki hello sanal makineleri (gelen trafiği) tarafından alınan bayt sayısı|
|Ağ dışına|Ağ dışına|Bayt|Toplam|Merhaba out tüm ağ arabirimlerindeki hello sanal makineleri (giden trafiği) tarafından bayt sayısı|
|Disk okuma bayt|Disk okuma bayt|Bayt|Toplam|İzleme süresi sırasında diskten okunan toplam bayt sayısı|
|Disk yazma bayt|Disk yazma bayt|Bayt|Toplam|İzleme süresi sırasında toodisk yazılan toplam bayt|
|Disk okuma işlemleri/sn|Disk okuma işlemleri/sn|CountPerSecond|Ortalama|Disk okuma IOPS|
|Disk yazma işlemi/sn|Disk yazma işlemi/sn|CountPerSecond|Ortalama|Disk yazma IOPS|

## <a name="microsoftcomputevirtualmachinescalesetsvirtualmachines"></a>Microsoft.Compute/virtualMachineScaleSets/virtualMachines

|Ölçüm|Ölçüm görünen adı|Birim|Toplama türü|Açıklama|
|---|---|---|---|---|
|CPU yüzdesi|CPU yüzdesi|Yüzde|Ortalama|şu anda hello sanal makineleri tarafından kullanılmakta olan ayrılmış işlem birimleri Hello yüzdesi|
|Ağ içine|Ağ içine|Bayt|Toplam|Merhaba tüm ağ arabirimlerindeki hello sanal makineleri (gelen trafiği) tarafından alınan bayt sayısı|
|Ağ dışına|Ağ dışına|Bayt|Toplam|Merhaba out tüm ağ arabirimlerindeki hello sanal makineleri (giden trafiği) tarafından bayt sayısı|
|Disk okuma bayt|Disk okuma bayt|Bayt|Toplam|İzleme süresi sırasında diskten okunan toplam bayt sayısı|
|Disk yazma bayt|Disk yazma bayt|Bayt|Toplam|İzleme süresi sırasında toodisk yazılan toplam bayt|
|Disk okuma işlemleri/sn|Disk okuma işlemleri/sn|CountPerSecond|Ortalama|Disk okuma IOPS|
|Disk yazma işlemi/sn|Disk yazma işlemi/sn|CountPerSecond|Ortalama|Disk yazma IOPS|

## <a name="microsoftcustomerinsightshubs"></a>Microsoft.CustomerInsights/hubs

|Ölçüm|Ölçüm görünen adı|Birim|Toplama türü|Açıklama|
|---|---|---|---|---|
|DCIApiCalls|Müşteri Öngörüler API çağrıları|Sayı|Toplam||
|DCIMappingImportOperationSuccessfulLines|Eşleme içeri aktarma işlemi başarılı satırları|Sayı|Toplam||
|DCIMappingImportOperationFailedLines|Satırları alma işlemi eşleme işlemi başarısız oldu|Sayı|Toplam||
|DCIMappingImportOperationTotalLines|Eşleme içeri aktarma işlemi toplam satırları|Sayı|Toplam||
|DCIMappingImportOperationRuntimeInSeconds|Eşleme alma işlemi çalışma zamanı saniye cinsinden|Saniye|Toplam||
|DCIOutboundProfileExportSucceeded|Giden profili dışarı aktarma başarılı oldu|Sayı|Toplam||
|DCIOutboundProfileExportFailed|Giden profili dışarı aktarma başarısız oldu|Sayı|Toplam||
|DCIOutboundProfileExportDuration|Giden profili verme süresi|Saniye|Toplam||
|DCIOutboundKpiExportSucceeded|Giden KPI dışarı aktarma başarılı oldu|Sayı|Toplam||
|DCIOutboundKpiExportFailed|Giden KPI verme başarısız oldu|Sayı|Toplam||
|DCIOutboundKpiExportDuration|Giden KPI verme süresi|Saniye|Toplam||
|DCIOutboundKpiExportStarted|Giden KPI verme başlatıldı|Saniye|Toplam||
|DCIOutboundKpiRecordCount|Giden KPI kayıt sayısı|Saniye|Toplam||
|DCIOutboundProfileExportCount|Giden profil verme sayısı|Saniye|Toplam||
|DCIOutboundInitialProfileExportFailed|Giden ilk profili dışarı aktarma başarısız oldu|Saniye|Toplam||
|DCIOutboundInitialProfileExportSucceeded|Giden ilk profili dışarı aktarma başarılı oldu|Saniye|Toplam||
|DCIOutboundInitialKpiExportFailed|Giden ilk KPI verme başarısız oldu|Saniye|Toplam||
|DCIOutboundInitialKpiExportSucceeded|Giden ilk KPI dışarı aktarma başarılı oldu|Saniye|Toplam||
|DCIOutboundInitialProfileExportDurationInSeconds|Giden ilk profil verme süresini saniye cinsinden|Saniye|Toplam||
|AdlaJobForStandardKpiFailed|Saniye cinsinden başarısız standart KPI için adla işi|Saniye|Toplam||
|AdlaJobForStandardKpiTimeOut|Standart KPI saniye olarak zaman aşımı için adla işi|Saniye|Toplam||
|AdlaJobForStandardKpiCompleted|Saniye cinsinden tamamlandı standart KPI için adla işi|Saniye|Toplam||
|ImportASAValuesFailed|İçeri aktarma ASA değerleri sayımı başarısız oldu|Sayı|Toplam||
|ImportASAValuesSucceeded|İçeri aktarma ASA değerleri Count başarılı oldu|Sayı|Toplam||

## <a name="microsoftdatalakeanalyticsaccounts"></a>Microsoft.DataLakeAnalytics/accounts

|Ölçüm|Ölçüm görünen adı|Birim|Toplama türü|Açıklama|
|---|---|---|---|---|
|JobEndedSuccess|Başarılı işler|Sayı|Toplam|Başarılı işlerin sayısı.|
|JobEndedFailure|Başarısız olan işler|Sayı|Toplam|Başarısız olan işler sayısı.|
|JobEndedCancelled|İptal edilen işler|Sayı|Toplam|İptal edilen işlerin sayısı.|
|JobAUEndedSuccess|Başarılı AU zamanı|Saniye|Toplam|Toplam AU süredir başarılı işler.|
|JobAUEndedFailure|Başarısız AU zamanı|Saniye|Toplam|Başarısız olan işler toplam AU süresi.|
|JobAUEndedCancelled|İptal edilen AU zamanı|Saniye|Toplam|İptal edilen işler için toplam AU süre.|

## <a name="microsoftdbformysqlservers"></a>Microsoft.DBforMySQL/servers

|Ölçüm|Ölçüm görünen adı|Birim|Toplama türü|Açıklama|
|---|---|---|---|---|
|cpu_percent|CPU yüzdesi|Yüzde|Ortalama|CPU yüzdesi|
|compute_limit|Birim sınırı işlem|Sayı|Ortalama|Birim sınırı işlem|
|compute_consumption_percent|Birim yüzdesi işlem|Yüzde|Ortalama|Birim yüzdesi işlem|
|memory_percent|Bellek yüzdesi|Yüzde|Ortalama|Bellek yüzdesi|
|io_consumption_percent|G/ç yüzdesi|Yüzde|Ortalama|G/ç yüzdesi|
|storage_percent|Depolama yüzdesi|Yüzde|Ortalama|Depolama yüzdesi|
|storage_used|Kullanılan depolama|Bayt|Ortalama|Kullanılan depolama|
|storage_limit|Depolama sınırı|Bayt|Ortalama|Depolama sınırı|
|active_connections|Toplam etkin bağlantılar|Sayı|Ortalama|Toplam etkin bağlantılar|
|connections_failed|Toplam başarısız bağlantıları|Sayı|Ortalama|Toplam başarısız bağlantıları|

## <a name="microsoftdbforpostgresqlservers"></a>Microsoft.DBforPostgreSQL/servers

|Ölçüm|Ölçüm görünen adı|Birim|Toplama türü|Açıklama|
|---|---|---|---|---|
|cpu_percent|CPU yüzdesi|Yüzde|Ortalama|CPU yüzdesi|
|compute_limit|Birim sınırı işlem|Sayı|Ortalama|Birim sınırı işlem|
|compute_consumption_percent|Birim yüzdesi işlem|Yüzde|Ortalama|Birim yüzdesi işlem|
|memory_percent|Bellek yüzdesi|Yüzde|Ortalama|Bellek yüzdesi|
|io_consumption_percent|G/ç yüzdesi|Yüzde|Ortalama|G/ç yüzdesi|
|storage_percent|Depolama yüzdesi|Yüzde|Ortalama|Depolama yüzdesi|
|storage_used|Kullanılan depolama|Bayt|Ortalama|Kullanılan depolama|
|storage_limit|Depolama sınırı|Bayt|Ortalama|Depolama sınırı|
|active_connections|Toplam etkin bağlantılar|Sayı|Ortalama|Toplam etkin bağlantılar|
|connections_failed|Toplam başarısız bağlantıları|Sayı|Ortalama|Toplam başarısız bağlantıları|

## <a name="microsoftdevicesiothubs"></a>Microsoft.Devices/IotHubs

|Ölçüm|Ölçüm görünen adı|Birim|Toplama türü|Açıklama|
|---|---|---|---|---|
|d2c.telemetry.ingress.allProtocol|Telemetri ileti gönderme denemeleri|Sayı|Toplam|Gönderilen tooyour IOT hub cihaz bulut telemetri iletilerini denenen toobe sayısı|
|d2c.telemetry.ingress.Success|Gönderilen telemetri iletilerini|Sayı|Toplam|Başarıyla gönderilen tooyour IOT hub cihaz bulut telemetri iletilerini sayısı|
|c2d.Commands.egress.Complete.Success|Tamamlanan komutları|Sayı|Toplam|Merhaba aygıt tarafından başarıyla tamamlandı bulut cihaz komutlarının sayısı|
|c2d.Commands.egress.Abandon.Success|Terk komutları|Sayı|Toplam|Merhaba aygıt tarafından terk bulut cihaz komutlarının sayısı|
|c2d.Commands.egress.Reject.Success|Reddedilen komutları|Sayı|Toplam|Merhaba aygıt tarafından reddedilen bulut cihaz komutlarının sayısı|
|devices.totalDevices|Toplam aygıt|Sayı|Toplam|Tooyour IOT hub'ı kayıtlı aygıtların sayısı|
|devices.connectedDevices.allProtocol|Bağlı aygıtlar|Sayı|Toplam|Tooyour IOT hub'ı bağlı aygıt sayısı|
|d2c.telemetry.egress.Success|Telemetri iletilerini teslim|Sayı|Toplam|İletileri başarıyla tooendpoints (toplam) yazılmış sayısı|
|d2c.telemetry.egress.dropped|Bırakılan iletiler|Sayı|Toplam|Merhaba teslim endpoint ölü olduğundan bırakılan ileti sayısı|
|d2c.telemetry.egress.orphaned|Yalnız bırakılmış ileti|Sayı|Toplam|Merhaba hello geri dönüş yolu da dahil olmak üzere tüm yollar eşleşmeyen ileti sayısı|
|d2c.telemetry.egress.invalid|Geçersiz iletileri|Sayı|Toplam|Merhaba ileti sayısı nedeniyle teslim edilmedi tooincompatibility hello uç noktası ile|
|d2c.telemetry.egress.fallback|Geri dönüş koşulla eşleşen iletileri|Sayı|Toplam|Toohello geri dönüş endpoint yazılan ileti sayısı|
|d2c.endpoints.egress.eventHubs|Hub uç noktaları tooEvent iletiler teslim|Sayı|Toplam|İletileri başarıyla yazılı tooEvent Hub uç noktaları olan sayısı|
|d2c.endpoints.latency.eventHubs|Olay hub'ı uç noktaları için ileti gecikme süresi|milisaniye|Ortalama|Merhaba ortalama gecikme süresi ileti giriş toohello IOT hub ve ileti giriş arasındaki milisaniye cinsinden bir olay hub'ı uç içine|
|d2c.endpoints.egress.serviceBusQueues|İleti veri yolu kuyruğu uç noktaları tooService teslim|Sayı|Toplam|İletileri başarıyla yazılı tooService veri yolu kuyruğu uç noktaları olan sayısı|
|d2c.endpoints.latency.serviceBusQueues|Hizmet veri yolu kuyruğu uç noktalar için ileti gecikme süresi|milisaniye|Ortalama|Merhaba ortalama gecikme süresi ileti giriş toohello IOT hub ve ileti giriş arasındaki milisaniye olarak bir hizmet veri yolu kuyruğu uç noktası içine|
|d2c.endpoints.egress.serviceBusTopics|İleti veri yolu konusu uç noktaları tooService teslim|Sayı|Toplam|İletileri başarıyla yazılı tooService veri yolu konusu uç noktaları olan sayısı|
|d2c.endpoints.latency.serviceBusTopics|Hizmet veri yolu konusu uç noktalar için ileti gecikme süresi|milisaniye|Ortalama|Merhaba ortalama gecikme süresi ileti giriş toohello IOT hub ve ileti giriş arasındaki milisaniye olarak bir hizmet veri yolu konusu uç noktası içine|
|d2c.endpoints.egress.builtIn.events|Toohello yerleşik uç noktası (iletileri/olayları) teslim edilen ileti|Sayı|Toplam|İletileri başarıyla yazılı toohello yerleşik uç noktası (iletileri/olayları) olan sayısı|
|d2c.endpoints.latency.builtIn.events|İleti gecikme hello yerleşik uç noktası (iletileri/olayları) için|milisaniye|Ortalama|Merhaba ortalama gecikme süresi arasında ileti giriş toohello IOT hub ve ileti giriş hello yerleşik uç noktası (iletileri/olayları), milisaniye cinsinden içine |
|d2c.Twin.Read.Success|Başarılı twin aygıtlardan okur|Sayı|Toplam|tüm başarılı aygıt tarafından başlatılan twin Hello sayısını okur.|
|d2c.Twin.Read.failure|Aygıtlardan Twin okuma başarısız oldu|Sayı|Toplam|Merhaba sayımını tüm aygıt tarafından başlatılan twin okuma başarısız oldu.|
|d2c.Twin.Read.size|Aygıtlardan twin yanıt boyutu okur|Bayt|Ortalama|Merhaba ortalama, min ve max tüm başarılı değeri aygıt tarafından başlatılan okuma çifti.|
|d2c.Twin.Update.Success|Aygıtlardan başarılı twin güncelleştirmeleri|Sayı|Toplam|Merhaba tüm başarılı twin aygıt tarafından başlatılan güncelleştirme sayısı.|
|d2c.Twin.Update.failure|Aygıtlardan Twin güncelleştirmeler başarısız oldu|Sayı|Toplam|Merhaba sayımını tüm aygıt tarafından başlatılan twin güncelleştirmeler başarısız oldu.|
|d2c.Twin.Update.size|Aygıtlardan twin güncelleştirmeleri boyutu|Bayt|Ortalama|Merhaba ortalama, min ve max boyutu tüm başarılı aygıt tarafından başlatılan güncelleştirmeleri çifti.|
|c2d.methods.Success|Başarılı doğrudan yöntem çağrıları|Sayı|Toplam|tüm başarılı doğrudan yöntem çağrılarını Hello sayısı.|
|c2d.methods.failure|Doğrudan yöntem çağrılarını başarısız oldu|Sayı|Toplam|Tüm Hello sayısı doğrudan yöntem çağrıları başarısız oldu.|
|c2d.methods.requestSize|Doğrudan yöntem çağrılarını isteği boyutu|Bayt|Ortalama|Merhaba ortalama, min ve max tüm başarılı doğrudan yöntemi istekleri.|
|c2d.methods.responseSize|Doğrudan yöntem çağrılarını yanıt boyutu|Bayt|Ortalama|Merhaba ortalama, min ve max tüm başarılı doğrudan yöntem yanıtların.|
|c2d.Twin.Read.Success|Arka ucunuzdan başarılı twin okur|Sayı|Toplam|tüm başarılı arka uç başlatılan twin Hello sayısını okur.|
|c2d.Twin.Read.failure|Arka ucunuzdan başarısız twin okur|Sayı|Toplam|Merhaba sayımını tüm arka uç başlatılan twin okuma başarısız oldu.|
|c2d.Twin.Read.size|Arka uç twin okuma yanıt boyutu|Bayt|Ortalama|Merhaba ortalama, min ve max tüm başarılı, arka uç başlatılan okuma çifti.|
|c2d.Twin.Update.Success|Arka uç başarılı twin güncelleştirmeleri|Sayı|Toplam|Merhaba tüm başarılı twin arka uç başlatılan güncelleştirme sayısı.|
|c2d.Twin.Update.failure|Arka uç başarısız twin güncelleştirmeleri|Sayı|Toplam|Merhaba sayımını tüm arka uç başlatılan twin güncelleştirmeler başarısız oldu.|
|c2d.Twin.Update.size|Arka uç twin güncelleştirmelerini boyutu|Bayt|Ortalama|Merhaba ortalama, min ve max boyutu tüm başarılı arka uç başlatılan güncelleştirmeleri çifti.|
|twinQueries.success|Başarılı twin sorguları|Sayı|Toplam|tüm başarılı twin sorguları Hello sayısı.|
|twinQueries.failure|Başarısız twin sorguları|Sayı|Toplam|Tüm başarısız twin sorguları Hello sayısı.|
|twinQueries.resultSize|Twin sorguları sonuç boyutu|Bayt|Ortalama|Hello ortalama, min ve max hello sonuç boyutunun tüm başarılı twin sorgular.|
|jobs.createTwinUpdateJob.success|Twin güncelleştirme işlerinin başarılı oluşturma|Sayı|Toplam|tüm başarılı twin güncelleştirme işlerinin oluşturulması Hello sayısı.|
|jobs.createTwinUpdateJob.failure|Twin güncelleştirme işlerinin başarısız oluşturma|Sayı|Toplam|tüm oluşturma işlemi başarısız twin güncelleştirme işleri Hello sayısı.|
|jobs.createDirectMethodJob.success|Yöntem çağırma işlerinin başarılı oluşturma|Sayı|Toplam|tüm başarılı doğrudan yöntemi çağırma işlerinin oluşturulması Hello sayısı.|
|jobs.createDirectMethodJob.failure|Yöntem çağırma işlerinin başarısız oluşturma|Sayı|Toplam|tüm oluşturma işlemi başarısız doğrudan yöntem çağrısını işler Hello sayısı.|
|jobs.listJobs.success|Başarılı çağrı toolist işleri|Sayı|Toplam|tüm başarılı çağrı toolist işleri Hello sayısı.|
|jobs.listJobs.failure|Başarısız çağrılar toolist işleri|Sayı|Toplam|Tüm başarısız çağrılar toolist işleri Hello sayısı.|
|jobs.cancelJob.success|Başarılı iş iptalleri|Sayı|Toplam|Merhaba sayımını tüm başarılı bir işi toocancel çağırır.|
|jobs.cancelJob.failure|Başarısız iş iptalleri|Sayı|Toplam|Tüm başarısız çağrılar toocancel bir işi Hello sayısı.|
|jobs.queryJobs.success|İş başarılı sorguları|Sayı|Toplam|tüm başarılı çağrı tooquery işleri Hello sayısı.|
|jobs.queryJobs.failure|Başarısız işi sorgular|Sayı|Toplam|Tüm başarısız çağrılar tooquery işleri Hello sayısı.|
|Jobs.Completed|Tamamlanan İşler|Sayı|Toplam|Tüm tamamlanan işler Hello sayısı.|
|Jobs.Failed|Başarısız olan işler|Sayı|Toplam|Tüm başarısız işler Hello sayısı.|
|d2c.telemetry.ingress.sendThrottle|Azaltma hatalarının sayısı|Sayı|Toplam|Toodevice verimlilik kısıtlamaları nedeniyle azaltma hatalarının sayısı|
|dailyMessageQuotaUsed|Kullanılan iletilerin toplam sayısı|Sayı|Ortalama|Günümüzde kullanılan toplam ileti sayısı|

## <a name="microsofteventhubnamespaces"></a>Microsoft.EventHub/namespaces

|Ölçüm|Ölçüm görünen adı|Birim|Toplama türü|Açıklama|
|---|---|---|---|---|
|INREQS|Gelen gönderme isteği|Sayı|Toplam|Toplam gelen istekleri bir bildirim hub'ı Gönder|
|SUCCREQ|Başarılı istekler|Sayı|Toplam|Bir ad alanı için toplam başarılı istekler|
|FAILREQ|Başarısız istekler|Sayı|Toplam|Bir ad alanı için toplam başarısız istek sayısı|
|SVRBSY|Sunucu meşgul hataları|Sayı|Toplam|Bir ad alanı için toplam sunucu meşgul hataları|
|INTERR|İç sunucu hataları|Sayı|Toplam|Bir ad alanı için toplam iç sunucu hataları|
|MISCERR|Diğer hatalar|Sayı|Toplam|Bir ad alanı için toplam başarısız istek sayısı|
|INMSGS|Gelen iletileri|Sayı|Toplam|Bir ad alanı için toplam gelen iletileri|
|OUTMSGS|Giden iletiler|Sayı|Toplam|Toplam Giden iletiler için bir ad alanı|
|EHINMBS|Gelen bayt sayısı|Bayt|Toplam|Olay hub'ı bir ad alanı için gelen ileti işleme|
|EHOUTMBS|Giden bayt sayısı|Bayt|Toplam|Toplam Giden iletiler için bir ad alanı|
|EHABL|Arşiv biriktirme listesi iletileri|Sayı|Toplam|Olay hub'ı arşiv iletileri bir ad alanı için biriktirme listesi|
|EHAMSGS|Mesajları arşivleme|Sayı|Toplam|Olay hub'ı Arşivlenmiş bir ad alanındaki iletileri|
|EHAMBS|Arşiv ileti işleme|Bayt|Toplam|Bir ad alanında olay hub'ı arşivlenmiş ileti işleme|

## <a name="microsoftlogicworkflows"></a>Microsoft.Logic/workflows

|Ölçüm|Ölçüm görünen adı|Birim|Toplama türü|Açıklama|
|---|---|---|---|---|
|RunsStarted|Başlatılan çalıştırır|Sayı|Toplam|Başlatılan iş akışı çalıştırma sayısı.|
|RunsCompleted|Tamamlanan çalıştırır|Sayı|Toplam|Tamamlanan iş akışı çalıştırma sayısı.|
|RunsSucceeded|Başarılı bir şekilde çalışır|Sayı|Toplam|Başarılı iş akışı çalıştırma sayısı.|
|RunsFailed|Başarısız çalıştırır|Sayı|Toplam|Başarısız iş akışı çalıştırma sayısı.|
|RunsCancelled|İptal çalıştırır|Sayı|Toplam|İptal edilen iş akışı çalıştırma sayısı.|
|RunLatency|Gecikme çalıştırın|Saniye|Ortalama|Tamamlanan iş akışı çalıştırmalarının gecikme süresi.|
|RunSuccessLatency|Başarı gecikme çalıştırın|Saniye|Ortalama|Başarılı iş akışı çalıştırmalarının gecikme süresi.|
|RunThrottledEvents|Daraltılmış olayları çalıştırın|Sayı|Toplam|İş akışı eylemi veya tetikleyiciyle kısıtlanan olay sayısı.|
|RunFailurePercentage|Hata yüzdesi çalıştırın|Yüzde|Toplam|İş akışı yüzdesi başarısız çalışır.|
|ActionsStarted|Başlatılan Eylemler |Sayı|Toplam|Başlatılan iş akışı eylemi sayısı.|
|ActionsCompleted|Eylemler tamamlandı |Sayı|Toplam|Tamamlanan iş akışı eylemi sayısı.|
|ActionsSucceeded|Eylemler başarılı oldu |Sayı|Toplam|Başarılı iş akışı eylemi sayısı.|
|ActionsFailed|Eylemler başarısız oldu|Sayı|Toplam|Başarısız iş akışı eylemi sayısı.|
|ActionsSkipped|Atlanan Eylemler |Sayı|Toplam|Atlanan iş akışı eylemi sayısı.|
|ActionLatency|Eylem gecikme süresi |Saniye|Ortalama|Tamamlanan iş akışı eylemlerinin gecikme süresi.|
|ActionSuccessLatency|Eylem başarı gecikme süresi |Saniye|Ortalama|Başarılı iş akışı eylemlerinin gecikme süresi.|
|ActionThrottledEvents|Eylem olayları kısıtlanan|Sayı|Toplam|İş akışı eylemi kısıtlanan olay sayısı.|
|TriggersStarted|Tetikleyiciler başlatıldı |Sayı|Toplam|Başlatılan iş akışı tetikleyicisi sayısı.|
|TriggersCompleted|Tetikleyiciler tamamlandı |Sayı|Toplam|Tamamlanan iş akışı tetikleyicisi sayısı.|
|TriggersSucceeded|Tetikleyiciler başarılı oldu |Sayı|Toplam|Başarılı iş akışı tetikleyicisi sayısı.|
|TriggersFailed|Tetikleyiciler başarısız oldu |Sayı|Toplam|Başarısız iş akışı tetikleyicisi sayısı.|
|TriggersSkipped|Atlanan Tetikleyicileri|Sayı|Toplam|Atlanan iş akışı tetikleyicisi sayısı.|
|TriggersFired|Harekete Tetikleyicileri |Sayı|Toplam|Harekete geçirilen iş akışı tetikleyicisi sayısı.|
|TriggerLatency|Tetikleme gecikmesi |Saniye|Ortalama|Tamamlanan iş akışı tetikleyicilerinin gecikmesi.|
|TriggerFireLatency|Tetikleyici yangın gecikme süresi |Saniye|Ortalama|Başlatılan iş akışı tetikleyicilerinin gecikmesi.|
|TriggerSuccessLatency|Tetikleyici başarı gecikme süresi |Saniye|Ortalama|Başarılı iş akışı tetikleyicilerinin gecikmesi.|
|TriggerThrottledEvents|Daraltılmış olaylarını tetiklemek|Sayı|Toplam|İş akışı tetikleyicisiyle kısıtlanan olay sayısı.|
|BillableActionExecutions|Faturalanabilir eylem yürütmeleri|Sayı|Toplam|İş akışı eylemi yürütmeleri faturalandırılır sayısı.|
|BillableTriggerExecutions|Faturalanabilir tetikleyici yürütmeleri|Sayı|Toplam|İş akışı tetikleyici yürütmeleri faturalandırılır sayısı.|
|TotalBillableExecutions|Toplam Faturalanabilir yürütmeleri|Sayı|Toplam|İş akışı yürütmeleri faturalandırılır sayısı.|

## <a name="microsoftnetworkapplicationgateways"></a>Microsoft.Network/applicationGateways

|Ölçüm|Ölçüm görünen adı|Birim|Toplama türü|Açıklama|
|---|---|---|---|---|
|Aktarım hızı|Aktarım hızı|BytesPerSecond|Ortalama||

## <a name="microsoftnetworkexpressroutecircuits"></a>Microsoft.Network/expressRouteCircuits

|Ölçüm|Ölçüm görünen adı|Birim|Toplama türü|Açıklama|
|---|---|---|---|---|
|BytesIn|BytesIn|Sayı|Toplam||
|BytesOut|BytesOut|Sayı|Toplam||

## <a name="microsoftnotificationhubsnamespacesnotificationhubs"></a>Microsoft.NotificationHubs/Namespaces/NotificationHubs

|Ölçüm|Ölçüm görünen adı|Birim|Toplama türü|Açıklama|
|---|---|---|---|---|
|registration.all|Kayıt işlemi|Sayı|Toplam|tüm başarılı kayıt işlemleri (oluşturma güncelleştirmeleri sorgular ve silme işlemleri) Hello sayısı. |
|registration.Create|Kayıt oluşturma işlemleri|Sayı|Toplam|tüm başarılı kaydı oluşturmaları Hello sayısı.|
|registration.Update|Kayıt Güncelleme işlemleri|Sayı|Toplam|Merhaba tüm başarılı kaydı güncelleştirme sayısı.|
|registration.get|Kayıt okuma işlemleri|Sayı|Toplam|tüm başarılı kaydı sorguları Hello sayısı.|
|registration.Delete|Kayıt silme işlemleri|Sayı|Toplam|tüm başarılı kaydı silme işlemleri Hello sayısı.|
|gelen|Gelen iletileri|Sayı|Toplam|tüm başarılı Hello sayısı API çağrıları gönderin. |
|incoming.Scheduled|Gönderilen zamanlanan anında iletme bildirimleri|Sayı|Toplam|İptal zamanlanmış anında iletme bildirimleri|
|incoming.Scheduled.Cancel|İptal zamanlanmış anında iletme bildirimleri|Sayı|Toplam|İptal zamanlanmış anında iletme bildirimleri|
|Scheduled.Pending|Bekleyen zamanlanmış bildirimleri|Sayı|Toplam|Bekleyen zamanlanmış bildirimleri|
|installation.all|Yükleme yönetim işlemleri|Sayı|Toplam|Yükleme yönetim işlemleri|
|installation.get|Yükleme işlemleri Al|Sayı|Toplam|Yükleme işlemleri Al|
|installation.upsert|Yükleme İşlemleri Oluştur veya Güncelleştir|Sayı|Toplam|Yükleme İşlemleri Oluştur veya Güncelleştir|
|installation.Patch|Düzeltme eki yükleme işlemleri|Sayı|Toplam|Düzeltme eki yükleme işlemleri|
|installation.Delete|Yükleme işlemlerini sil|Sayı|Toplam|Yükleme işlemlerini sil|
|outgoing.allpns.Success|Başarılı bildirimler|Sayı|Toplam|tüm başarılı bildirimler Hello sayısı.|
|outgoing.allpns.invalidpayload|Yük hataları|Sayı|Toplam|Merhaba PNS bir bozuk yükü hata döndürdüğünden başaramayan iter Hello sayısı.|
|outgoing.allpns.pnserror|Harici bildirim sistemi hataları|Sayı|Toplam|Merhaba PNS (kimlik doğrulama sorunları hiç tutar) ile iletişim kurulurken bir sorun olduğundan, başarısız iter Hello sayısı.|
|outgoing.allpns.channelerror|Kanal hataları|Sayı|Toplam|Merhaba sayımını hello uygulama süresi dolmuş veya kısıtlanan doğru ile ilişkili olmayan hello kanal geçersiz olduğundan dolayı başarısız iter.|
|outgoing.allpns.badorexpiredchannel|Hatalı veya Süresi Dolmuş Kanal Hataları|Sayı|Toplam|Merhaba sayımını hello kanal/token/RegistrationId hello kaydında süresi dolmuş veya geçersiz olduğundan başarısız iter.|
|outgoing.WNS.Success|WNS başarılı bildirimler|Sayı|Toplam|tüm başarılı bildirimler Hello sayısı.|
|outgoing.WNS.invalidcredentials|WNS yetkilendirme hataları (geçersiz kimlik bilgileri)|Sayı|Toplam|Merhaba sayımını hello PNS kimlik bilgileri veya hello kimlik engellenen hello sağlanan kabul etmedi olmadığından başarısız iter. (Windows Live hello kimlik bilgilerini tanımıyor).|
|outgoing.WNS.badchannel|WNS geçersiz kanal hatası|Sayı|Toplam|Merhaba hello ChannelURI hello kaydında tanınmadığı için başarısız olan gönderim sayısı (WNS durumu: 404 bulunamadı).|
|outgoing.WNS.expiredchannel|WNS süresi dolan kanal hatası|Sayı|Toplam|Merhaba hello ChannelURI süresi dolduğundan, başarısız gönderim sayısı (WNS durumu: 410 Gone).|
|outgoing.WNS.throttled|WNS kısıtlanan bildirimler|Sayı|Toplam|Merhaba WNS bu uygulamayı azaltma nedeniyle başarısız olan gönderim sayısı (WNS durumu: 406 Kabul edilebilir değil).|
|outgoing.WNS.tokenproviderunreachable|WNS yetkilendirme hataları (ulaşılamıyor)|Sayı|Toplam|Windows Live ulaşılabilir değil.|
|outgoing.WNS.invalidtoken|WNS yetkilendirme hataları (geçersiz belirteç)|Sayı|Toplam|Merhaba belirteci tooWNS geçersiz sağlanan (WNS durumu: 401 yetkilendirilmedi).|
|outgoing.WNS.wrongtoken|WNS yetkilendirme hataları (yanlış belirteç)|Sayı|Toplam|tooWNS geçerli olması koşuluyla, ancak başka bir uygulama için belirteç Hello (WNS durumu: 403 Yasak). Hello ChannelURI hello kayıt başka bir uygulama ile ilişkili ise bu durum oluşabilir. Denetleyin, hello istemci uygulaması hello ile ilişkili kimlik bilgilerini hello bildirim hub ' aynı uygulama.|
|outgoing.WNS.invalidnotificationformat|WNS geçersiz bildirim biçimi|Sayı|Toplam|Merhaba bildirim Hello biçimi geçersiz (WNS durumu: 400). WNS tüm geçersiz yüklerini Reddet değil unutmayın.|
|outgoing.WNS.invalidnotificationsize|WNS Geçersiz Bildirim Biçimi Hatası|Sayı|Toplam|Merhaba bildirim yükü çok büyük (WNS durumu: 413).|
|outgoing.WNS.channelthrottled|WNS kanal kısıtlandı|Sayı|Toplam|Merhaba bildirim hello ChannelURI hello kaydında kısıtlanan olmadığından bırakıldı (WNS yanıt üstbilgisi: X-WNS-NotificationStatus:channelThrottled).|
|outgoing.WNS.channeldisconnected|WNS kanal bağlantısı kesildi|Sayı|Toplam|Merhaba bildirim hello ChannelURI hello kaydında kısıtlanan olmadığından bırakıldı (WNS yanıt üstbilgisi: X WNS DeviceConnectionStatus: bağlantısı kesilmiş).|
|outgoing.WNS.dropped|WNS bırakılan bildirimler|Sayı|Toplam|Merhaba bildirim hello ChannelURI hello kaydında kısıtlanan olmadığından bırakıldı (X WNS NotificationStatus: bırakılan ancak değil X-WNS-DeviceConnectionStatus: bağlantısı kesilmiş).|
|outgoing.WNS.pnserror|WNS hataları|Sayı|Toplam|Bildirim WNS ile iletişim hataları nedeniyle teslim edilmedi.|
|outgoing.WNS.authenticationerror|WNS kimlik doğrulama hataları|Sayı|Toplam|Windows Live geçersiz kimlik bilgileri veya yanlış belirteç ile iletişim hataları nedeniyle teslim edilmedi bildirimi.|
|outgoing.apns.Success|APNS başarılı bildirimler|Sayı|Toplam|tüm başarılı bildirimler Hello sayısı.|
|outgoing.apns.invalidcredentials|APNS yetkilendirme hataları|Sayı|Toplam|Merhaba sayımını hello PNS kimlik bilgileri veya hello kimlik engellenen hello sağlanan kabul etmedi olmadığından başarısız iter.|
|outgoing.apns.badchannel|APNS geçersiz kanal hatası|Sayı|Toplam|Merhaba hello belirteci geçersiz olduğundan başarısız oldu gönderim sayısı (APNS durum kodu: 8).|
|outgoing.apns.expiredchannel|APNS süresi dolan kanal hatası|Sayı|Toplam|Merhaba APNS geri bildirim kanalı tarafından geçersiz kılındı belirteci Hello sayısı.|
|outgoing.apns.invalidnotificationsize|APNS Geçersiz Bildirim Boyutu Hatası|Sayı|Toplam|Merhaba hello yükü çok büyük olduğu için başarısız olan gönderim sayısı (APNS durum kodu: 7).|
|outgoing.apns.pnserror|APNS hataları|Sayı|Toplam|Merhaba sayımını APNS ile iletişim hataları nedeniyle başarısız olan iter.|
|outgoing.GCM.Success|GCM başarılı bildirimler|Sayı|Toplam|tüm başarılı bildirimler Hello sayısı.|
|outgoing.GCM.invalidcredentials|GCM yetkilendirme hataları (geçersiz kimlik bilgileri)|Sayı|Toplam|Merhaba sayımını hello PNS kimlik bilgileri veya hello kimlik engellenen hello sağlanan kabul etmedi olmadığından başarısız iter.|
|outgoing.GCM.badchannel|GCM geçersiz kanal hatası|Sayı|Toplam|Merhaba hello RegistrationId hello kaydında tanınmadığı için başarısız olan gönderim sayısı (GCM sonucu: Geçersiz kaydı).|
|outgoing.GCM.expiredchannel|GCM süresi dolan kanal hatası|Sayı|Toplam|Merhaba hello RegistrationId hello kaydında süresi dolduğu için başarısız olan gönderim sayısı (GCM sonucu: NotRegistered).|
|outgoing.GCM.throttled|GCM kısıtlanan bildirimler|Sayı|Toplam|Merhaba bu uygulamayı GCM kısıtlanan nedeniyle başarısız olan gönderim sayısı (GCM durum kodu: 501-599 veya sonucu: kullanılamaz).|
|outgoing.GCM.invalidnotificationformat|GCM geçersiz bildirim biçimi|Sayı|Toplam|Merhaba hello yükü doğru biçimlendirilmedi nedeniyle başarısız olan gönderim sayısı (GCM sonucu: InvalidDataKey veya InvalidTtl).|
|outgoing.GCM.invalidnotificationsize|GCM Geçersiz Bildirim Boyutu Hatası|Sayı|Toplam|Merhaba hello yükü çok büyük olduğu için başarısız olan gönderim sayısı (GCM sonucu: MessageTooBig).|
|outgoing.GCM.wrongchannel|GCM yanlış kanal hatası|Sayı|Toplam|Merhaba RegistrationId hello kaydında olmadığı için başarısız olan iter Hello sayısı ilişkili toohello geçerli uygulama (GCM sonucu: InvalidPackageName).|
|outgoing.GCM.pnserror|GCM hataları|Sayı|Toplam|Merhaba sayımını GCM ile iletişim hataları nedeniyle başarısız olan iter.|
|outgoing.GCM.authenticationerror|GCM kimlik doğrulama hataları|Sayı|Toplam|Merhaba PNS kabul etmedi hello sağlanan kimlik bilgileri hello kimlik engellendi hello veya hello Senderıd hello uygulamada düzgün yapılandırılmadığı için başarısız olan gönderim sayısı (GCM sonucu: MismatchedSenderId).|
|outgoing.mpns.Success|MPNS başarılı bildirimler|Sayı|Toplam|tüm başarılı bildirimler Hello sayısı.|
|outgoing.mpns.invalidcredentials|MPNS geçersiz kimlik bilgileri|Sayı|Toplam|Merhaba sayımını hello PNS kimlik bilgileri veya hello kimlik engellenen hello sağlanan kabul etmedi olmadığından başarısız iter.|
|outgoing.mpns.badchannel|MPNS geçersiz kanal hatası|Sayı|Toplam|Merhaba hello ChannelURI hello kaydında tanınmadığı için başarısız olan gönderim sayısı (MPNS durumu: 404 bulunamadı).|
|outgoing.mpns.throttled|MPNS kısıtlanan bildirimler|Sayı|Toplam|Merhaba MPNS bu uygulamayı azaltma nedeniyle başarısız olan gönderim sayısı (WNS MPNS: 406 Kabul edilebilir değil).|
|outgoing.mpns.invalidnotificationformat|MPNS geçersiz bildirim biçimi|Sayı|Toplam|Merhaba sayımını hello hello bildirim yükü çok büyük olduğu için başarısız olan iter.|
|outgoing.mpns.channeldisconnected|MPNS kanalın bağlantısı kesildi|Sayı|Toplam|Merhaba hello ChannelURI hello kaydında kesildiği için başarısız olan gönderim sayısı (MPNS durumu: 412 bulunamadı).|
|outgoing.mpns.dropped|MPNS bırakılan bildirimler|Sayı|Toplam|Merhaba tarafından MPNS bırakılan gönderim sayısı (MPNS yanıt üstbilgisi: X NotificationStatus: QueueFull veya Suppressed).|
|outgoing.mpns.pnserror|MPNS hataları|Sayı|Toplam|Merhaba sayımını MPNS ile iletişim hataları nedeniyle başarısız olan iter.|
|outgoing.mpns.authenticationerror|MPNS kimlik doğrulama hataları|Sayı|Toplam|Merhaba sayımını hello PNS kimlik bilgileri veya hello kimlik engellenen hello sağlanan kabul etmedi olmadığından başarısız iter.|
|notificationhub.pushes|Tüm giden bildirimleri|Sayı|Toplam|Merhaba bildirim hub'ın tüm giden bildirimleri|
|incoming.all.Requests|Tüm gelen istekleri|Sayı|Toplam|Bir bildirim hub'ı toplam gelen istekleri|
|incoming.all.failedrequests|Tüm gelen istekleri başarısız oldu|Sayı|Toplam|Bildirim hub'ı toplam gelen başarısız istekleri|

## <a name="microsoftpowerbidedicatedcapacities"></a>Microsoft.PowerBIDedicated/capacities

|Ölçüm|Ölçüm görünen adı|Birim|Toplama türü|Açıklama|
|---|---|---|---|---|
|qpu_metric|QPU|Sayı|Ortalama|QPU. S1, S2 için 0-200 ve 0-400 S4 için için 0-100 aralığında|
|memory_metric|Bellek|Bayt|Ortalama|Bellek. 0-25 GB S1, S2 için 0-50 GB ve 0-100 aralığında S4 için GB|
|TotalConnectionRequests|Toplam bağlantı istekleri|Sayı|Ortalama|Toplam bağlantı istekleri. Varış bunlar.|
|SuccessfullConnectionsPerSec|Başarılı bağlantıları sayısı / sn|CountPerSecond|Ortalama|Başarılı bağlantının tamamlamalar oranı.|
|TotalConnectionFailures|Toplam bağlantı hataları|Sayı|Ortalama|Toplam bağlantı denemesi başarısız oldu.|
|CurrentUserSessions|Geçerli kullanıcı oturumları|Sayı|Ortalama|Oluşturulan kullanıcı oturumları geçerli sayısı.|
|QueryPoolBusyThreads|Sorgu havuzu meşgul iş parçacıkları|Sayı|Ortalama|Meşgul hello sorgu iş parçacığı havuzu iş parçacıkları sayısı.|
|CommandPoolJobQueueLength|Komut havuzu iş sırası uzunluğu|Sayı|Ortalama|Merhaba komutu iş parçacığı havuzunun hello sırasındaki işlerin sayısı.|
|ProcessingPoolJobQueueLength|İşlem havuzu iş sırası uzunluğu|Sayı|Ortalama|İş parçacığı havuzu işleme hello hello sırasındaki olmayan-g/Ç işlerin sayısı.|
|CurrentConnections|Bağlantı: Geçerli bağlantılar|Sayı|Ortalama|İstemci bağlantı kuran geçerli sayısı.|
|CleanerCurrentPrice|Bellek: Temizleyici geçerli fiyatı|Sayı|Ortalama|Geçerli fiyat bellek, bayt / $/ saat, normalleştirilmiş too1000.|
|CleanerMemoryShrinkable|: Temizleyici bellek daraltılabilir|Bayt|Ortalama|Bellek miktarını bayt cinsinden hello arka plan temizleyici tarafından konu toopurging.|
|CleanerMemoryNonshrinkable|Bellek: Temizleyici bellek nonshrinkable|Bayt|Ortalama|Bellek miktarını bayt cinsinden konu toopurging hello arka plan temizleyici tarafından değil.|
|MemoryUsage|Bellek: Bellek kullanımı|Bayt|Ortalama|Temizleyici bellek fiyatı hesaplamak için kullanılan gibi hello sunucu işleminin bellek kullanımını. Bellek eşlemeli veri olan eşlenen veya hello xVelocity altyapısı bellek sınırı aşan hello xVelocity bellek içi analytics altyapısı (VertiPaq) tarafından ayrılan bellek yoksayılıyor toocounter Process\PrivateBytes artı hello boyutu eşit.|
|MemoryLimitHard|Bellek: Sabit bellek sınırı|Bayt|Ortalama|Yapılandırma dosyasından sabit bellek sınırı.|
|MemoryLimitHigh|Bellek: Bellek sınırı yüksek|Bayt|Ortalama|Yapılandırma dosyasından yüksek bellek sınırı.|
|MemoryLimitLow|Bellek: Bellek sınırı düşük|Bayt|Ortalama|Yapılandırma dosyasından düşük bellek sınırı.|
|MemoryLimitVertiPaq|Bellek: Bellek sınırı VertiPaq|Bayt|Ortalama|Yapılandırma dosyasından bellek içi sınırı.|
|Kota|Bellek: Kota|Bayt|Ortalama|Bayt cinsinden geçerli bellek kotasını. Bellek kotasını bellek grant veya bellek ayırma de denir.|
|QuotaBlocked|Bellek: Engellenen kota|Sayı|Ortalama|Geçerli diğer bellek kotalarını serbest kadar engellenen kota istek sayısı.|
|VertiPaqNonpaged|Bellek: VertiPaq belleği olmayan havuz|Bayt|Ortalama|Bayt bellek kullanmak için hello çalışma kümesindeki hello bellek içi altyapısı tarafından kilitlenmiş.|
|VertiPaqPaged|Bellek: Disk belleği VertiPaq|Bayt|Ortalama|Bellek içi veriler için kullanılan disk belleği bayt.|
|RowsReadPerSec|İşlem: Satır sayısı / sn okuyun.|CountPerSecond|Ortalama|Satır oranını tüm ilişkisel veritabanlarından okuyun.|
|RowsConvertedPerSec|İşlem: Satır sayısı / sn dönüştürülür.|CountPerSecond|Ortalama|İşleme sırasında dönüştürülmüş satır oranı.|
|RowsWrittenPerSec|İşlem: saniye yazılan satırları|CountPerSecond|Ortalama|İşleme sırasında yazılmış satırları oranı.|
|CommandPoolBusyThreads|İş parçacıkları: Komut havuzu meşgul iş parçacıkları|Sayı|Ortalama|Meşgul hello komutu iş parçacığı havuzu iş parçacıkları sayısı.|
|CommandPoolIdleThreads|İş parçacıkları: boş iş parçacığı havuzu komutu|Sayı|Ortalama|Merhaba komutu iş parçacığı havuzundaki boş iş parçacığı sayısı.|
|LongParsingBusyThreads|İş parçacıkları: meşgul iş parçacığı ayrıştırma uzun|Sayı|Ortalama|İş parçacığı havuzu uzun ayrıştırma hello meşgul iş parçacığı sayısı.|
|LongParsingIdleThreads|İş parçacıkları: boş iş parçacığı ayrıştırma uzun|Sayı|Ortalama|İş parçacığı havuzu uzun ayrıştırma hello boş iş parçacığı sayısı.|
|LongParsingJobQueueLength|İş parçacıkları: Uzun iş kuyruğu uzunluğu ayrıştırma|Sayı|Ortalama|İş parçacığı havuzu uzun ayrıştırma hello hello sırasındaki işlerin sayısı.|
|ProcessingPoolBusyIOJobThreads|İş parçacıkları: havuz meşgul g/ç iş iş parçacığı işleme|Sayı|Ortalama|Çalışan iş parçacığı havuzu işleme hello g/ç iş iş parçacığı sayısı.|
|ProcessingPoolBusyNonIOThreads|İş parçacıkları: yoğun olmayan-g/Ç iş parçacığı havuzu işleme|Sayı|Ortalama|Çalışan iş parçacığı havuzu işleme hello olmayan-g/Ç iş iş parçacığı sayısı.|
|ProcessingPoolIOJobQueueLength|İş parçacıkları: işleme havuzu g/ç iş sırası uzunluğu|Sayı|Ortalama|İş parçacığı havuzu işleme hello hello sırasındaki g/ç işlerin sayısı.|
|ProcessingPoolIdleIOJobThreads|İş parçacıkları: havuz boşta g/ç iş iş parçacığı işleme|Sayı|Ortalama|İş parçacığı havuzu işleme hello g/ç işleri için boş iş parçacığı sayısı.|
|ProcessingPoolIdleNonIOThreads|İş parçacıkları: boş olmayan-g/Ç iş parçacığı havuzu işleme|Sayı|Ortalama|İş parçacığı havuzu işleme hello içindeki boş iş parçacığı sayısı toonon-g/Ç işleri ayrılmış.|
|QueryPoolIdleThreads|İş parçacıkları: Sorgu havuzu boşta iş parçacıkları|Sayı|Ortalama|İş parçacığı havuzu işleme hello g/ç işleri için boş iş parçacığı sayısı.|
|QueryPoolJobQueueLength|İş parçacıkları: Sorgu havuzu iş kuyruğu lengt|Sayı|Ortalama|Merhaba sorgu iş parçacığı havuzunun hello sırasındaki işlerin sayısı.|
|ShortParsingBusyThreads|İş parçacıkları: meşgul iş parçacığı ayrıştırma kısa|Sayı|Ortalama|İş parçacığı havuzu ayrıştırma kısa hello meşgul iş parçacığı sayısı.|
|ShortParsingIdleThreads|İş parçacıkları: boş iş parçacığı ayrıştırma kısa|Sayı|Ortalama|İş parçacığı havuzu ayrıştırma kısa hello boş iş parçacığı sayısı.|
|ShortParsingJobQueueLength|İş parçacıkları: İş kuyruğu uzunluğu ayrıştırma kısa|Sayı|Ortalama|İş parçacığı havuzu ayrıştırma kısa hello hello sırasındaki işlerin sayısı.|
|memory_thrashing_metric|Bellek yoğun disk belleği|Yüzde|Ortalama|Ortalama bellek yoğun disk belleği'ü tıklatın.|

## <a name="microsoftsearchsearchservices"></a>Microsoft.Search/searchServices

|Ölçüm|Ölçüm görünen adı|Birim|Toplama türü|Açıklama|
|---|---|---|---|---|
|SearchLatency|Arama gecikme süresi|Saniye|Ortalama|Merhaba arama hizmeti için ortalama arama gecikme süresi|
|SearchQueriesPerSecond|Saniye başına arama sorguları|CountPerSecond|Ortalama|Arama sorguları hello arama hizmeti için saniye başına|
|ThrottledSearchQueriesPercentage|Daraltılmış arama sorguları yüzdesi|Yüzde|Ortalama|Merhaba arama hizmeti için kısıtlanan arama sorguları yüzdesi|

## <a name="microsoftservicebusnamespaces"></a>Microsoft.ServiceBus/namespaces

|Ölçüm|Ölçüm görünen adı|Birim|Toplama türü|Açıklama|
|---|---|---|---|---|
|CPUXNS|Ad alanı başına CPU kullanımı|Yüzde|Maksimum|Service bus premium ad alanı CPU kullanım ölçümü|
|WSXNS|Ad alanı başına bellek boyutu kullanımı|Yüzde|Maksimum|Service bus premium ad alanı bellek kullanım ölçümü|

## <a name="microsoftsqlserversdatabases"></a>Microsoft.Sql/servers/databases

|Ölçüm|Ölçüm görünen adı|Birim|Toplama türü|Açıklama|
|---|---|---|---|---|
|cpu_percent|CPU yüzdesi|Yüzde|Ortalama|CPU yüzdesi|
|physical_data_read_percent|Veri G/Ç yüzdesi|Yüzde|Ortalama|Veri G/Ç yüzdesi|
|log_write_percent|Günlük g/ç yüzdesi|Yüzde|Ortalama|Günlük g/ç yüzdesi|
|dtu_consumption_percent|DTU yüzdesi|Yüzde|Ortalama|DTU yüzdesi|
|Depolama|Toplam veritabanı boyutu|Bayt|Maksimum|Toplam veritabanı boyutu|
|connection_successful|Başarılı bağlantıları|Sayı|Toplam|Başarılı bağlantıları|
|connection_failed|Başarısız bağlantı sayısı|Sayı|Toplam|Başarısız bağlantı sayısı|
|blocked_by_firewall|Güvenlik Duvarı tarafından engellendi|Sayı|Toplam|Güvenlik Duvarı tarafından engellendi|
|Kilitlenme|Kilitlenmeleri|Sayı|Toplam|Kilitlenmeleri|
|storage_percent|Veri boyutu yüzdesi|Yüzde|Maksimum|Veri boyutu yüzdesi|
|xtp_storage_percent|Bellek içi OLTP depolama yüzdesi|Yüzde|Ortalama|Bellek içi OLTP depolama yüzdesi|
|workers_percent|Çalışanlar yüzdesi|Yüzde|Ortalama|Çalışanlar yüzdesi|
|sessions_percent|Oturumları yüzdesi|Yüzde|Ortalama|Oturumları yüzdesi|
|dtu_limit|DTU sınırı|Sayı|Ortalama|DTU sınırı|
|dtu_used|Kullanılan DTU|Sayı|Ortalama|Kullanılan DTU|
|dwu_limit|DWU sınırı|Sayı|Maksimum|DWU sınırı|
|dwu_consumption_percent|DWU yüzdesi|Yüzde|Maksimum|DWU yüzdesi|
|dwu_used|Kullanılan DWU|Sayı|Maksimum|Kullanılan DWU|

## <a name="microsoftsqlserverselasticpools"></a>Microsoft.Sql/servers/elasticPools

|Ölçüm|Ölçüm görünen adı|Birim|Toplama türü|Açıklama|
|---|---|---|---|---|
|cpu_percent|CPU yüzdesi|Yüzde|Ortalama|CPU yüzdesi|
|database_cpu_percent|CPU yüzdesi|Yüzde|Ortalama|CPU yüzdesi|
|physical_data_read_percent|Veri G/Ç yüzdesi|Yüzde|Ortalama|Veri G/Ç yüzdesi|
|database_physical_data_read_percent|Veri G/Ç yüzdesi|Yüzde|Ortalama|Veri G/Ç yüzdesi|
|log_write_percent|Günlük g/ç yüzdesi|Yüzde|Ortalama|Günlük g/ç yüzdesi|
|database_log_write_percent|Günlük g/ç yüzdesi|Yüzde|Ortalama|Günlük g/ç yüzdesi|
|dtu_consumption_percent|DTU yüzdesi|Yüzde|Ortalama|DTU yüzdesi|
|database_dtu_consumption_percent|DTU yüzdesi|Yüzde|Ortalama|DTU yüzdesi|
|storage_percent|Depolama yüzdesi|Yüzde|Ortalama|Depolama yüzdesi|
|workers_percent|Çalışanlar yüzdesi|Yüzde|Ortalama|Çalışanlar yüzdesi|
|database_workers_percent|Çalışanlar yüzdesi|Yüzde|Ortalama|Çalışanlar yüzdesi|
|sessions_percent|Oturumları yüzdesi|Yüzde|Ortalama|Oturumları yüzdesi|
|database_sessions_percent|Oturumları yüzdesi|Yüzde|Ortalama|Oturumları yüzdesi|
|eDTU_limit|eDTU sınırı|Sayı|Ortalama|eDTU sınırı|
|storage_limit|Depolama sınırı|Bayt|Ortalama|Depolama sınırı|
|eDTU_used|kullanılan eDTU|Sayı|Ortalama|kullanılan eDTU|
|storage_used|Kullanılan depolama|Bayt|Ortalama|Kullanılan depolama|
|database_storage_used|Kullanılan depolama|Bayt|Ortalama|Kullanılan depolama|
|xtp_storage_percent|Bellek içi OLTP depolama yüzdesi|Yüzde|Ortalama|Bellek içi OLTP depolama yüzdesi|

## <a name="microsoftsqlservers"></a>Microsoft.Sql/servers

|Ölçüm|Ölçüm görünen adı|Birim|Toplama türü|Açıklama|
|---|---|---|---|---|
|dtu_consumption_percent|DTU yüzdesi|Yüzde|Ortalama|DTU yüzdesi|
|database_dtu_consumption_percent|DTU yüzdesi|Yüzde|Ortalama|DTU yüzdesi|
|storage_used|Kullanılan depolama|Bayt|Ortalama|Kullanılan depolama|
|database_storage_used|Kullanılan depolama|Bayt|Ortalama|Kullanılan depolama|

## <a name="microsoftstreamanalyticsstreamingjobs"></a>Microsoft.StreamAnalytics/streamingjobs

|Ölçüm|Ölçüm görünen adı|Birim|Toplama türü|Açıklama|
|---|---|---|---|---|
|ResourceUtilization|SU % kullanımı|Yüzde|Maksimum|SU % kullanımı|
|InputEvents|Giriş olayları|Sayı|Toplam|Giriş olayları|
|InputEventBytes|Giriş olayı bayt|Bayt|Toplam|Giriş olayı bayt|
|LateInputEvents|Geç giriş olayları|Sayı|Toplam|Geç giriş olayları|
|OutputEvents|Çıkış olayları|Sayı|Toplam|Çıkış olayları|
|ConversionErrors|Veri dönüştürme hataları|Sayı|Toplam|Veri dönüştürme hataları|
|Hatalar|Çalışma zamanı hataları|Sayı|Toplam|Çalışma zamanı hataları|
|DroppedOrAdjustedEvents|Bozuk olayları|Sayı|Toplam|Bozuk olayları|
|AMLCalloutRequests|İşlev istekleri|Sayı|Toplam|İşlev istekleri|
|AMLCalloutFailedRequests|Başarısız işleve istekleri|Sayı|Toplam|Başarısız işleve istekleri|
|AMLCalloutInputEvents|İşlev olayları|Sayı|Toplam|İşlev olayları|

## <a name="microsoftwebserverfarms"></a>Microsoft.Web/serverfarms

|Ölçüm|Ölçüm görünen adı|Birim|Toplama türü|Açıklama|
|---|---|---|---|---|
|CpuPercentage|CPU Yüzdesi|Yüzde|Ortalama|CPU Yüzdesi|
|MemoryPercentage|Bellek yüzdesi|Yüzde|Ortalama|Bellek yüzdesi|
|DiskQueueLength|Disk Sırası Uzunluğu|Sayı|Toplam|Disk Sırası Uzunluğu|
|HttpQueueLength|HTTP sırası uzunluğu|Sayı|Toplam|HTTP sırası uzunluğu|
|BytesReceived|Verileri|Bayt|Toplam|Verileri|
|BytesSent|Giden veriler|Bayt|Toplam|Giden veriler|

## <a name="microsoftwebsites-excluding-functions"></a>Microsoft.Web/sites (işlevler hariç)

|Ölçüm|Ölçüm görünen adı|Birim|Toplama türü|Açıklama|
|---|---|---|---|---|
|CPU zamanı|CPU süresi|Saniye|Toplam|CPU süresi|
|İstekler|İstekler|Sayı|Toplam|İstekler|
|BytesReceived|Verileri|Bayt|Toplam|Verileri|
|BytesSent|Giden veriler|Bayt|Toplam|Giden veriler|
|Http101|HTTP 101|Sayı|Toplam|HTTP 101|
|Http2xx|HTTP 2xx|Sayı|Toplam|HTTP 2xx|
|Http3xx|HTTP 3xx|Sayı|Toplam|HTTP 3xx|
|Http401|HTTP 401|Sayı|Toplam|HTTP 401|
|Http403|HTTP 403|Sayı|Toplam|HTTP 403|
|Http404|HTTP 404|Sayı|Toplam|HTTP 404|
|Http406|HTTP 406|Sayı|Toplam|HTTP 406|
|Http4xx|HTTP 4xx|Sayı|Toplam|HTTP 4xx|
|Http5xx|HTTP sunucu hataları|Sayı|Toplam|HTTP sunucu hataları|
|MemoryWorkingSet|Bellek çalışma kümesi|Bayt|Ortalama|Bellek çalışma kümesi|
|AverageMemoryWorkingSet|Ortalama bellek çalışma kümesi|Bayt|Ortalama|Ortalama bellek çalışma kümesi|
|AverageResponseTime|Ortalama yanıt süresi|Saniye|Ortalama|Ortalama yanıt süresi|

## <a name="microsoftwebsites-functions"></a>Microsoft.Web/sites (işlev)

|Ölçüm|Ölçüm görünen adı|Birim|Toplama türü|Açıklama|
|---|---|---|---|---|
|BytesReceived|Verileri|Bayt|Toplam|Verileri|
|BytesSent|Giden veriler|Bayt|Toplam|Giden veriler|
|Http5xx|HTTP sunucu hataları|Sayı|Toplam|HTTP sunucu hataları|
|MemoryWorkingSet|Bellek çalışma kümesi|Bayt|Ortalama|Bellek çalışma kümesi|
|AverageMemoryWorkingSet|Ortalama bellek çalışma kümesi|Bayt|Ortalama|Ortalama bellek çalışma kümesi|
|FunctionExecutionUnits|İşlev yürütme birimleri|Sayı|Ortalama|İşlev yürütme birimleri|
|İşlev yürütme sayısı|İşlev yürütme sayısı|Sayı|Ortalama|İşlev yürütme sayısı|

## <a name="microsoftwebsitesslots"></a>Microsoft.Web/sites/slots

|Ölçüm|Ölçüm görünen adı|Birim|Toplama türü|Açıklama|
|---|---|---|---|---|
|CPU zamanı|CPU süresi|Saniye|Toplam|CPU süresi|
|İstekler|İstekler|Sayı|Toplam|İstekler|
|BytesReceived|Verileri|Bayt|Toplam|Verileri|
|BytesSent|Giden veriler|Bayt|Toplam|Giden veriler|
|Http101|HTTP 101|Sayı|Toplam|HTTP 101|
|Http2xx|HTTP 2xx|Sayı|Toplam|HTTP 2xx|
|Http3xx|HTTP 3xx|Sayı|Toplam|HTTP 3xx|
|Http401|HTTP 401|Sayı|Toplam|HTTP 401|
|Http403|HTTP 403|Sayı|Toplam|HTTP 403|
|Http404|HTTP 404|Sayı|Toplam|HTTP 404|
|Http406|HTTP 406|Sayı|Toplam|HTTP 406|
|Http4xx|HTTP 4xx|Sayı|Toplam|HTTP 4xx|
|Http5xx|HTTP sunucu hataları|Sayı|Toplam|HTTP sunucu hataları|
|MemoryWorkingSet|Bellek çalışma kümesi|Bayt|Ortalama|Bellek çalışma kümesi|
|AverageMemoryWorkingSet|Ortalama bellek çalışma kümesi|Bayt|Ortalama|Ortalama bellek çalışma kümesi|
|AverageResponseTime|Ortalama yanıt süresi|Saniye|Ortalama|Ortalama yanıt süresi|
|FunctionExecutionUnits|İşlev yürütme birimleri|Sayı|Ortalama|İşlev yürütme birimleri|
|İşlev yürütme sayısı|İşlev yürütme sayısı|Sayı|Ortalama|İşlev yürütme sayısı|

## <a name="next-steps"></a>Sonraki adımlar
* [Azure İzleyicisi'nde ölçümleri hakkında bilgi edinin](monitoring-overview-metrics.md)
* [Ölçümleri uyarı oluşturma](insights-receive-alert-notifications.md)
* [Ölçümleri toostorage, olay hub'ı ya da günlük analizi dışarı aktarma](monitoring-overview-of-diagnostic-logs.md)
