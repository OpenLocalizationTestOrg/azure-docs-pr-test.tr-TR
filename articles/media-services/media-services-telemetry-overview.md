---
title: Medya Hizmetleri Telemetri aaaAzure | Microsoft Docs
description: "Bu makalede Azure Media Services telemetri genel bir bakış sağlar."
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 95c20ec4-c782-4063-8042-b79f95741d28
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/29/2017
ms.author: juliako
ms.openlocfilehash: 659e1c947a77aad0e4acacb541d95714da4775ee
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-media-services-telemetry"></a>Telemetri Azure medya Hizmetleri

Azure Media Services (AMS) hizmetlerinin tooaccess telemetri/ölçüm verilerini sağlar. AMS Hello geçerli sürümü için telemetri verileri Canlı toplamanıza olanak sağlar **kanal**, **StreamingEndpoint**ve canlı **arşiv** varlıklar. 

Telemetri, belirttiğiniz bir Azure depolama hesabında tooa depolama tablosu yazılır (genellikle, AMS hesabınızla ilişkili hello depolama hesabı kullanırsınız). 

Merhaba telemetri sistem veri saklama yönetmez. Merhaba depolama tabloları silerek hello eski telemetri verilerini kaldırabilirsiniz.

Bu konuda ele alınmıştır nasıl tooconfigure ve hello AMS telemetri kullanabilir.

## <a name="configuring-telemetry"></a>Telemetri yapılandırma

Bir bileşen düzeyinde ayrıntı telemetri yapılandırabilirsiniz. İki ayrıntı düzeyi "Normal" ve "Ayrıntılı" vardır. Şu anda, her iki düzeyleri hello dönüş aynı bilgileri. Toouse "Normal. önerilir. 

konuları göster nasıl aşağıdaki hello tooenable telemetri:

[.NET ile telemetri etkinleştirme](media-services-dotnet-telemetry.md) 

[REST telemetriyle etkinleştirme](media-services-rest-telemetry.md)

## <a name="consuming-telemetry-information"></a>Telemetri bilgileri kullanma

Telemetri telemetri hello Media Services hesabı için yapılandırıldığında, belirttiğiniz hello depolama hesabındaki tooan Azure depolama tablosu yazılır. Bu bölümde hello depolama tabloları hello ölçümünün açıklanmaktadır.

Telemetri verileri yolları aşağıdaki hello birinde kullanmasını sağlayabilirsiniz:

- Verileri doğrudan Azure Table (örneğin hello depolama SDK'sını kullanarak) depolama alanından okuyun. Merhaba telemetri depolama tabloları Hello açıklaması için bkz **telemetri bilgileri tüketen** içinde [bu](https://msdn.microsoft.com/library/mt742089.aspx) konu.

Veya

- Merhaba desteğini hello Media Services .NET SDK'sı depolama verileri okumak için açıklandığı gibi kullanmak [bu](media-services-dotnet-telemetry.md) konu. 


aşağıda açıklanan hello telemetri şema iyi bir performans tasarlanmış toogive Azure Table Storage hello sınırları içinde verilmiştir:

- Veri Hizmeti Kimliğinde ve hesabı tarafından bölümlenmiş bağımsız olarak sorgulanan her hizmet toobe tooallow telemetrisinden.
- Bölümler hello tarih toogive bir makul hello bölüm boyutu üst sınırı içerir.
- Satır anahtarları ters zaman sipariş tooallow hello en son telemetri öğeleri toobe içinde belirli bir hizmeti için sorgulanır.

Bu çoğu hello ortak sorguları toobe verimli izin vermesi gerekir:

- Paralel, bağımsız veri ayrı Hizmetleri Yükleniyor.
- Bir tarih aralığındaki belirli bir hizmeti için tüm veriler alınıyor.
- Bir hizmet için en son verileri Hello alınıyor.

### <a name="telemetry-table-storage-output-schema"></a>Telemetri tablo depolama çıkış şeması

Telemetri verileri bir tabloda "TelemetryMetrics20160321 burada tarih oluşturulan Merhaba tablonun"20160321"," aggregate depolanır. Telemetri sistem yeni her gün 00:00 UTC temel için ayrı bir tablo oluşturur. Merhaba tablo kullanılır toostore yinelenen değerleri gibi belirli bir pencere süresi, gönderilen bayt sayısı, vb. içinde bit hızı alma. 

Özellik|Değer|Örnekler/notları
---|---|---
PartitionKey|{Hesap Kimliği} _ {varlık kimliği}|e49bef329c29495f9b9570989682069d_64435281c50a4dd8ab7011cb0f4cdf66 < br /<br/>Merhaba kimliği burada birden çok Media Services hesabı yazma toohello hello bölüm anahtarı toosimplify iş akışlarında dahil hesabı aynı depolama hesabı.
RowKey|{saniye toomidnight} _ {rastgele bir değeri}|01688_00199<br/><br/>Merhaba satır anahtarı bölüm içinde saniye toomidnight tooallow üst n stili sorguları hello sayısı başlar. Daha fazla bilgi için bkz: [bu](../cosmos-db/table-storage-design-guide.md#log-tail-pattern) makalesi. 
zaman damgası|Tarih/saat|Zaman damgası hello Azure tablo 2016'dan otomatik-09-09T22:43:42.241Z
Tür|telemetri verileri sağlayan hello varlığın Hello türü|StreamingEndpoint/kanal/arşiv<br/><br/>Olay türü yalnızca bir dize değeridir.
Ad|Merhaba telemetri olay Hello adı|ChannelHeartbeat/StreamingEndpointRequestLog
ObservedTime|(UTC) Hello zaman hello telemetri olayı oluştu|2016-09-09T22:42:36.924Z<br/><br/>Merhaba zaman hello varlık hello telemetri göndermeyi tarafından (örneğin bir kanal) sağlanan gözlenen. Bu değer için bileşenler arasındaki eşitleme sorunlarını yaklaşık bir saat olabilir
ServiceId|{Hizmet kimliği}|f70bd731-691d-41c6-8f2d-671d0bdc9c7e
Varlık özgü özellikleri|Merhaba olayı tarafından tanımlanan|StreamName: stream1, bit hızı 10123...<br/><br/>Merhaba kalan özellikleri olay türü verilen hello için tanımlanır. Azure tablo anahtar değer çifti içeriktir.  (diğer bir deyişle, hello tablodaki farklı satırlarla farklı özellik kümelerine sahip).

### <a name="entity-specific-schema"></a>Varlık özgü şeması

Her sıklığı aşağıdaki hello ile gönderilen varlık özgü telemetric veri girişi üç tür vardır:

- Akış uç noktaları: her 30 saniye
- Canlı kanallar: dakikada
- Canlı arşiv: dakikada

**Akış uç noktası**

Özellik|Değer|Örnekler
---|---|---
PartitionKey|PartitionKey|e49bef329c29495f9b9570989682069d_64435281c50a4dd8ab7011cb0f4cdf66
RowKey|RowKey|01688_00199
zaman damgası|zaman damgası|Zaman damgası Azure tablo 2016'dan otomatik-09-09T22:43:42.241Z
Tür|Tür|StreamingEndpoint
Ad|Ad|StreamingEndpointRequestLog
ObservedTime|ObservedTime|2016-09-09T22:42:36.924Z
ServiceId|Hizmet kimliği|f70bd731-691d-41c6-8f2d-671d0bdc9c7e
Ana bilgisayar adı|Merhaba uç noktasının ana bilgisayar adı|builddemoserver.origin.mediaservices.Windows.NET
statusCode|HTTP kayıtlar durumu|200
ResultCode|Sonuç kodu ayrıntısı|S_OK
RequestCount|Merhaba toplama toplam istek|3
BytesSent|Gönderilen toplam bayt sayısı|2987358
ServerLatency|Ortalama sunucu gecikme süresi (depolama alanıyla birlikte)|129
E2ELatency|Ortalama uçtan uca gecikme süresi|250

**Canlı kanal**

Özellik|Değer|Örnekler/notları
---|---|---
PartitionKey|PartitionKey|e49bef329c29495f9b9570989682069d_64435281c50a4dd8ab7011cb0f4cdf66
RowKey|RowKey|01688_00199
zaman damgası|zaman damgası|Zaman damgası hello Azure tablo 2016'dan otomatik-09-09T22:43:42.241Z
Tür|Tür|Kanal
Ad|Ad|ChannelHeartbeat
ObservedTime|ObservedTime|2016-09-09T22:42:36.924Z
ServiceId|Hizmet kimliği|f70bd731-691d-41c6-8f2d-671d0bdc9c7e
TrackType|İzleme video/ses/metin türü|video/ses
TrackName|Merhaba izleme adı|Video/audio_1
Bit hızı|İzleme bit hızı|785000
CustomAttributes||   
IncomingBitrate|Gerçek gelen bit hızı|784548
OverlapCount|Merhaba örtüşme alma|0
DiscontinuityCount|Süreksizlik izlemek için|0
LastTimestamp|En son alınan veri zaman damgası|1800488800
NonincreasingCount|Zaman damgası toonon artırma atılan parça sayısı|2
UnalignedKeyFrames|(Kalitesi düzeylerini) fragment(s) aldık olup olmadığını hizalı değil çerçeveler burada anahtar |True
UnalignedPresentationTime|Olup fragment(s) (kalitesi düzeylerini/parçaları arasında) burada sunu zamanını hizalanmadıysa aldık|True
UnexpectedBitrate|Ses/video için hesaplanan/gerçek hızı > en fazla 40.000 bps ve IncomingBitrate izlerseniz doğru == veya IncomingBitrate ve actualBitrate % 50 farklı 0 |True
Sorunsuz|Gerekirse true, <br/>overlapCount, <br/>DiscontinuityCount, <br/>NonIncreasingCount, <br/>UnalignedKeyFrames, <br/>UnalignedPresentationTime, <br/>UnexpectedBitrate<br/> Tüm 0|True<br/><br/>Koşullar tutma aşağıdaki hello hiçbirini olduğunda false döndürür birleşik bir işlev iyi durumda:<br/><br/>-OverlapCount > 0<br/>-DiscontinuityCount > 0<br/>-NonincreasingCount > 0<br/>-UnalignedKeyFrames gerekmektedir<br/>-UnalignedPresentationTime gerekmektedir<br/>-UnexpectedBitrate gerekmektedir

**Canlı arşiv**

Özellik|Değer|Örnekler/notları
---|---|---
PartitionKey|PartitionKey|e49bef329c29495f9b9570989682069d_64435281c50a4dd8ab7011cb0f4cdf66
RowKey|RowKey|01688_00199
zaman damgası|zaman damgası|Zaman damgası hello Azure tablo 2016'dan otomatik-09-09T22:43:42.241Z
Tür|Tür|Arşiv
Ad|Ad|ArchiveHeartbeat
ObservedTime|ObservedTime|2016-09-09T22:42:36.924Z
ServiceId|Hizmet kimliği|f70bd731-691d-41c6-8f2d-671d0bdc9c7e
ManifestName|Program URL'si|asset-eb149703-ed0a-483c-91c4-e4066e72cce3/a0a5cfbf-71ec-4BD2-8c01-a92a2b38c9ba.ism
TrackName|Merhaba izleme adı|audio_1
TrackType|Merhaba izleme türü|Ses/video
CustomAttribute|Aynı ada sahip farklı izlemek ve bit hızı (çoklu Kamera Açısı) arasında ayıran dize onaltılı|
Bit hızı|İzleme bit hızı|785000
Sorunsuz|Gerekirse true, FragmentDiscardedCount == 0 & & ArchiveAcquisitionError == False|TRUE (Bu iki değer hello ölçümünde mevcut değildir ancak hello kaynak olayda var)<br/><br/>Koşullar tutma aşağıdaki hello hiçbirini olduğunda false döndürür birleşik bir işlev iyi durumda:<br/><br/>-FragmentDiscardedCount > 0<br/>-ArchiveAcquisitionError gerekmektedir

## <a name="general-qa"></a>Genel soru- cevap

### <a name="how-tooconsume-metrics-data"></a>Nasıl tooconsume ölçüm verilerini?

Ölçüm verilerini Azure tabloları bir dizi hello müşterinin depolama hesabındaki olarak depolanır. Bu veriler, araçları aşağıdaki hello kullanarak tüketilebilir:

- AMS SDK'SI
- Microsoft Azure Storage Gezgini (verme toocomma virgülle ayrılmış değer biçimindedir ve içinde işlenen Excel destekler)
- REST API

### <a name="how-toofind-average-bandwidth-consumption"></a>Nasıl toofind, bant genişliği tüketimi ortalama?

Merhaba ortalama bant genişliği tüketimi hello BytesSent zaman dilimi içinde ortalamasıdır.

### <a name="how-toodefine-streaming-unit-count"></a>Nasıl toodefine akış birimi sayısını?

Akış birim sayısını hello hello yoğun hello yoğun verimini bir akış uç noktası tarafından bölünmüş hello hizmetin akış uç noktalarını veri akışından olarak tanımlanabilir. Merhaba en yüksek kullanılabilir verimini bir akış uç noktası 160 MB / sn'dir.
Örneğin, bir müşterinin hizmetinden hello en yüksek verimlilik 40 MB/sn (Merhaba en büyük değerini BytesSent zaman dilimi üzerinden) olduğunu varsayın. Ardından, birim sayısı akış hello eşit too(40 MBps) * olduğu (8 bit/bayt) /(160 Mbps) 2 akış birimleri =.

### <a name="how-toofind-average-requestssecond"></a>Nasıl toofind ortalama istek/saniye?

toofind hello ortalama sayısı istek/saniye (RequestCount) isteklerinin ortalama sayısı hello zaman dilimi işlem.

### <a name="how-toodefine-channel-health"></a>Nasıl toodefine, sistem durumu kanal?

Aşağıdaki koşullar hello hiçbirini tuttuğunuzda yanlış olacak şekilde, kanal durumu bileşik Boolean işlevi olarak tanımlanabilir:

- OverlapCount > 0
- DiscontinuityCount > 0
- NonincreasingCount > 0
- UnalignedKeyFrames gerekmektedir 
- UnalignedPresentationTime gerekmektedir 
- UnexpectedBitrate gerekmektedir


### <a name="how-toodetect-discontinuities"></a>Nasıl toodetect discontinuities?

toodetect discontinuities Bul tüm kanal veri girişleri nerede DiscontinuityCount > 0. Merhaba karşılık gelen ObservedTime zaman damgası hello discontinuities gerçekleştiği hello kez gösterir.

### <a name="how-toodetect-timestamp-overlaps"></a>Nasıl toodetect zaman damgası çakışıyor?

toodetect zaman damgası çakışmalar Bul tüm kanal veri girişleri nerede OverlapCount > 0. Merhaba karşılık gelen ObservedTime zaman damgası hangi hello zaman damgası çakışıyor kez oluştu hello gösterir.

### <a name="how-toofind-streaming-request-failures-and-reasons"></a>Nasıl toofind akış istek hataları ve nedenleri?

toofind akış istek hataları ve nedeni, ResultCode eşit tooS_OK olduğu tüm akış uç noktası veri girişi bulun. Merhaba karşılık gelen StatusCode alan hello hello isteği başarısızlık nedeni gösterir.

### <a name="how-tooconsume-data-with-external-tools"></a>Nasıl harici araçlar tooconsume verilerle?

Telemetric veriler işlenir ve araçları aşağıdaki hello ile görselleştirilen:

- PowerBI
- Application Insights
- Azure İzleyicisi'ni (önceki adıyla Shoebox)
- AMS Canlı Panosu
- Azure Portal (bekleyen sürüm)

### <a name="how-toomanage-data-retention"></a>Nasıl toomanage veri saklama?

Merhaba telemetri sistem veri saklama Yönetimi veya otomatik silme eski kayıtları sağlamaz. Bu nedenle, toomanage gerekir ve eski kayıtları hello depolama tablosundan el ile silin. İçin nasıl toostorage SDK başvurabilir toodo onu.

## <a name="next-steps"></a>Sonraki adımlar

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Geri bildirimde bulunma

[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]
