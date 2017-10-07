---
title: "aaaAzure Media Services akış uç genel bakış | Microsoft Docs"
description: "Bu konu, akış uç noktaları Azure Media Services genel bakış sağlar."
services: media-services
documentationcenter: 
author: Juliako
writer: juliako
manager: cfowler
editor: 
ms.assetid: 097ab5e5-24e1-4e8e-b112-be74172c2701
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/29/2017
ms.author: juliako
ms.openlocfilehash: f27f590175dcc945d1d3299fc0cae5a68cfbf4e9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="streaming-endpoints-overview"></a>Akış uç noktaları genel bakış 

##<a name="overview"></a>Genel Bakış

Microsoft Azure Media Services (AMS) içinde bir **akış uç noktası** içerik doğrudan tooa istemci oynatıcı uygulaması ya da daha fazla dağıtım tooa içerik teslim ağı (CDN) teslim bir akış hizmetini temsil eder. Media Services, ayrıca Azure CDN entegrasyon sağlar. Merhaba giden akış StreamingEndpoint hizmetinden canlı akış, isteğe bağlı veya aşamalı indirme Media Services hesabınızda, varlık, bir video olabilir. Her Azure Media Services hesabı varsayılan StreamingEndpoint içerir. Ek akış hello hesabı altında oluşturulabilir. Akış, 1.0 ve 2. 0'ın iki sürümü vardır. 10 Ocak 2017 ile başlayarak, yeni oluşturulan tüm AMS hesapları sürüm 2.0 içerecektir **varsayılan** StreamingEndpoint. Aynı zamanda sürüm 2.0 akış uç noktaları toothis hesabı eklemek ek olacaktır. Bu değişiklik hello var olan hesapları etkilemez; Varolan akış sürüm 1.0 olacaktır ve yükseltilmiş tooversion 2.0 olabilir. Bu değişiklikle olacaktır davranışı, faturalama ve özellik değişiklikleri (Merhaba daha fazla bilgi için bkz: **türleri ve sürümleri akış** bölümünde belgelenen aşağıda).

Ayrıca, Azure Media Services (Ocak 2017 ' serbest) hello 2.15 sürümü ile başlayan özellikler toohello akış uç noktası varlık aşağıdaki hello eklenen: **CdnProvider**, **CdnProfile**,  **FreeTrialEndTime**, **StreamingEndpointVersion**. Bu özellikleri ayrıntılı bakış için bkz: [bu](https://docs.microsoft.com/rest/api/media/operations/streamingendpoint). 

Standart akış uç noktası, hello sizin için oluşturulur varsayılan Azure Media Services hesabı oluşturduğunuzda **durduruldu** durumu. Merhaba varsayılan akış uç noktası silinemiyor. Azure CDN kullanılabilirlik hedeflenen hello bölgede Hello bağlı olarak, yeni oluşturulan varsayılan varsayılan akış uç noktası da "StandardVerizon" CDN içerir sağlayıcısı tümleştirme. 

>[!NOTE]
>Azure CDN tümleştirme akış uç noktası hello başlamadan önce devre dışı bırakılabilir.

Bu konuda akış uç noktaları tarafından sağlanan hello ana işlevlerine genel bir bakış sağlar.

## <a name="streaming-types-and-versions"></a>Akış türleri ve sürümleri

### <a name="standardpremium-types-version-20"></a>Standart/Premium türleri (sürüm 2.0)

Medya Hizmetleri Hello Ocak 2017 sürüm ile başlayarak, iki akış türü vardır: **standart** ve **Premium**. Bu tür "2.0" Merhaba akış uç noktası sürümünde bir parçasıdır.

Tür|Açıklama
---|---
**Standart**|Merhaba senaryoları hello çoğunluğu için işe yaramayacaktır hello varsayılan seçenek budur.<br/>Bu seçenek, sabit sınırlı SLA almak için ilk 15, başlattıktan sonra gün akış uç noktası hello ücretsizdir.<br/>Birden fazla akış uç noktaları oluşturursanız, yalnızca hello ilk ilk 15 gün, bunları başlar başlamaz başkalarının faturalandırılır hello Merhaba ücretsiz biridir. <br/>Ücretsiz deneme sürümü yalnızca media services hesapları ve varsayılan akış uç noktası oluşturulan toonewly geçerli olduğunu unutmayın. Varolan akış uç noktalarını ve ayrıca oluşturulan akış uç noktalarını değil içerir ücretsiz deneme süresi bile bunlar tooversion 2.0 yükseltti veya sürüm 2.0 oluşturulur.
**Premium**|Bu seçenek daha yüksek ölçek veya denetim gerektiren profesyonel senaryolar için uygundur.<br/>Satın alınan premium akış birimi (SU) kapasite temel alarak değişken SLA, ayrılmış akış uç noktalarını yalıtılmış bir ortamda dinamik ve kaynaklar için rekabet değil.

Merhaba daha ayrıntılı bilgi için bkz: **karşılaştırmak akış türleri** bölümden.

### <a name="classic-type-version-10"></a>Klasik türü (sürüm 1.0)

Önceki toohello 10 Ocak 2017 sürüm AMS hesapları oluşturulan kullanıcılar için elinizde bir **Klasik** akış uç noktası türü. Bu tür akış uç noktası sürüm "1.0" Merhaba bir parçasıdır.

Varsa, **sürüm "1.0"** akış uç noktası olan > akış birimleri (SU), 1 premium = premium akış uç noktası olur ve tüm AMS özellikleri sağlar (Merhaba gibi **standart/Premium** türü) herhangi bir ek yapılandırma adımı.

>[!NOTE]
>**Klasik** akış uç noktaları (sürüm "1.0" ve 0 SU), sınırlı özellikleri sağlar ve bir SLA içermez. Toomigrate çok önerilir**standart** daha iyi bir deneyim ve toouse özellikleri gibi dinamik paketleme veya şifreleme ve hello ile gelen diğer özellikleri tooget yazın **standart** türü. toomigrate toohello **standart** yazın, Git toohello [Azure portal](https://portal.azure.com/) seçip **katılımı tooStandard**. Merhaba geçiş hakkında daha fazla bilgi için bkz: [geçiş](#migration-between-types) bölümü.
>
>Bu işlem geri alınamaz ve fiyatlandırma bir etkisi kaybolacağını unutmayın.
>
 
## <a name="comparing-streaming-types"></a>Akış türleri karşılaştırma

### <a name="versions"></a>Sürümler

|Tür|StreamingEndpointVersion|ScaleUnits|CDN|Faturalandırma|SLA| 
|--------------|----------|-----------------|-----------------|-----------------|-----------------|    
|Klasik|1.0|0|NA|Ücretsiz|NA|
|Standart Akış Uç Noktası|2.0|0|Evet|Ücretli|Evet|
|Premium Akış Birimleri|1.0|>0|Evet|Ücretli|Evet|
|Premium Akış Birimleri|2.0|>0|Evet|Ücretli|Evet|

### <a name="features"></a>Özellikler

Özellik|Standart|Premium
---|---|---
Ücretsiz ilk 15 gün| Evet |Hayır
Aktarım hızı |Azure CDN kullanılmadığında too600 Mbps. CDN ölçekler.|Birim (SU) akış başına 200 MB/sn. CDN ölçekler.
SLA | 99.9|99,9 (200 MB/sn SU başına).
CDN|Azure CDN, üçüncü taraf CDN ya da hiçbir CDN.|Azure CDN, üçüncü taraf CDN ya da hiçbir CDN.
Faturalama eşit olarak bölünür| Günlük|Günlük
Dinamik şifreleme|Evet|Evet
Dinamik paketleme|Evet|Evet
Ölçek|Otomatik hedeflenen toohello verimlilik ölçeklendirir.|Ek akış birimleri
IP filtre/G20/özel konak|Evet|Evet
Aşamalı indirme|Evet|Evet
Önerilen kullanımı |Senaryoları akış hello büyük bir çoğunluğu için önerilir.|Profesyonel kullanımı.<br/>Düşünüyorsanız standart ötesinde gereksinimlerine sahip olabilir. Eş zamanlı İzleyici boyutu 50.000 görüntüleyiciler büyük bekliyorsanız, bize (amsstreaming microsoft.com adresindeki) başvurun.


## <a name="migration-between-types"></a>Türleri arasında geçiş

Kaynak | çok| Eylem
---|---|---
Klasik|Standart|Tooopt bileşenini gereksinimi
Klasik|Premium| Ölçek (ek akış birimleri)
Standart/Premium|Klasik|Kullanılabilir değil (akış uç noktası sürüm 1.0 ise. Scaleunits ayar toochange tooclassic izin çok "0")
Standart (ile/CDN olmadan)|Premium hello ile aynı yapılandırmaları|Hello izin **başlatılan** durumu. (Azure portalı üzerinden)
Premium (ile/CDN olmadan)|Standart hello ile aynı yapılandırmaları|Hello izin **başlatılan** durum (aracılığıyla Azure portalı)
Standart (ile/CDN olmadan)|Premium ile farklı yapılandırma|Hello izin **durduruldu** durum (aracılığıyla Azure portalı). Hello çalışır durumda izin verilmiyor.
Premium (ile/CDN olmadan)|Standart farklı yapılandırma|Hello izin **durduruldu** durum (aracılığıyla Azure portalı). Hello çalışır durumda izin verilmiyor.
1.0 sürümünü SU > = 1 CDN ile|Standart/Premium hiçbir CDN ile|Hello izin **durduruldu** durumu. Hello izin verilmiyor **başlatılan** durumu.
1.0 sürümünü SU > = 1 CDN ile|Standart ile/CDN olmadan|Hello izin **durduruldu** durumu. Hello izin verilmiyor **başlatılan** durumu. Sürüm 1.0 oluşturulur ve başlatılan silinir ve yeni bir CDN olacaktır.
1.0 sürümünü SU > = 1 CDN ile|Premium ile/CDN olmadan|Hello izin **durduruldu** durumu. Hello izin verilmiyor **başlatılan** durumu. Klasik CDN oluşturulur ve başlatılan silinir ve yeni bir olacaktır.

## <a name="next-steps"></a>Sonraki adımlar
Media Services öğrenme yollarını gözden geçirin.

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Geri bildirimde bulunma
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

